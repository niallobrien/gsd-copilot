# 🚀 GSD (Get Shit Done) for GitHub Copilot

This repository uses a **Spec-Driven Development** framework called GSD. It forces GitHub Copilot to remain disciplined by using a persistent "Project Memory" stored in the `.gsd/` folder.

## 📁 The GSD Structure

The system relies on three core files that act as the source of truth:

- **`.gsd/PROJECT.md`**: The North Star. Goals, tech stack, and constraints.
- **`.gsd/ROADMAP.md`**: The Plan. Phases and atomic tasks.
- **`.gsd/STATE.md`**: The Memory. Completed features, known bugs, and technical debt.

---

## Installation

This will pull the required files from Github into your project.

### 1. Initialize sparse checkout

`git sparse-checkout init --cone`

### 2. Set the folders you want to pull

`git sparse-checkout set .github .gsd`

### 3. Add the GSD repo as a remote and pull

- `git remote add gsd-source https://github.com/your-username/your-gsd-repo.git`

- `git pull gsd-source main`

## 🛠 Setup

### 1. Enable Instruction Files

1. Open VS Code Settings (`Cmd+,` or `Ctrl+,`).
2. Search for `github.copilot.chat.codeGeneration.useInstructionFiles`.
3. Set it to **Enabled**.

### 2. Install Slash Commands

Ensure the `.github/prompts/` directory contains the `.prompt.md` files provided in the setup. These files enable custom `/` commands in your Copilot Chat.

To enable these commands for the GitHub CLI, run `gh extension install github/gh-copilot`.

---

## ⌨️ Slash Commands

Use these commands in the Copilot Chat window to manage your workflow:

| Command     | Action                                                                      |
| :---------- | :-------------------------------------------------------------------------- |
| `/init-gsd` | **Bootstrap:** Scans your code and creates the `.gsd/` files.               |
| `/plan`     | **Strategize:** Analyzes the active task and proposes a technical approach. |
| `/todo`     | **Execute:** Writes the code for the current active task.                   |
| `/state`    | **Sync:** Updates your progress and logs bugs in `STATE.md`.                |
| `/verify`   | **QA:** Checks code against the spec and suggests a commit message.         |

---

## 🔄 The Workflow Loop

1. **Initialize:** Start a project with `/init-gsd`.
2. **Set Active Task:** Ensure one item in `.gsd/ROADMAP.md` is marked as `**ACTIVE**`.
3. **Plan:** Run `/plan` to review the logic before writing code.
4. **Implement:** Run `/todo` to generate the implementation.
5. **Document:** Run `/state` to mark the task complete and log any new bugs.
6. **Commit:** Run `/verify` to ensure quality and get a commit message.

---

## 💡 Pro Tips

- **Keep it Pinned:** The `.prompt.md` files automatically "pin" your GSD files to the context. If Copilot seems lost, manually add `#` followed by the filename (e.g., `Refer to #STATE.md`).
- **Be Brutal:** If Copilot suggests something that violates `PROJECT.md`, tell it: "Check the project constraints in PROJECT.md and try again."
- **Atomic Tasks:** Keep tasks in `ROADMAP.md` small. If a task takes more than one `/todo` command, break it into sub-tasks.

---

# ⌨️ GSD for GitHub CLI

This section guides you on using GSD directly from your terminal using the GitHub Copilot CLI extension.

## 1. Prerequisites

Before using GSD in your terminal, ensure the GitHub Copilot CLI extension is ready.

1. **Install GitHub CLI:** [Download link](https://cli.github.com/)
2. **Install Copilot Extension:**
   `gh extension install github/gh-copilot`
3. **Authenticate:**
   `gh auth login`

---

## 2. CLI Command Reference

The `gh copilot` tool automatically reads your `.github/prompts/*.prompt.md` files. Use the `-t` (target/text) flag to call them.

- **Initialize:** `gh copilot chat -t "/init-gsd"`
- **Plan Task:** `gh copilot chat -t "/plan"`
- **Write Code:** `gh copilot chat -t "/todo"`
- **Sync State:** `gh copilot chat -t "/state"`
- **Verify Sync:** `gh copilot chat -t "/verify"`

---

## 3. Shell Shortcuts (The "Pro" Way)

Add these aliases to your `~/.zshrc` or `~/.bashrc` to make GSD feel like a native tool.

# GSD Workflow Shortcuts

- `alias gsd-init='gh copilot chat -t "/init-gsd"'`
- `alias gsd-plan='gh copilot chat -t "/plan"'`
- `alias gsd-todo='gh copilot chat -t "/todo"'`
- `alias gsd-state='gh copilot chat -t "/state"'`
- `alias gsd-verify='gh copilot chat -t "/verify"'`

Reload your config: `source ~/.zshrc` or `source ~/.bashrc`

---

## 4. Advanced CLI Workflows

### Auto-updating Documentation

You can pipe the AI output directly back into your GSD persistence files:
`gh copilot chat -t "/state" > .gsd/STATE.md`

### Headless Verification

Before pushing, run verification to catch discrepancies:
`gsd-verify`
