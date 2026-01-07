# Project State

## 🟢 Completed Features

- [Date]: Initialized repo and file structure.
- [Date]: Added basic file reading logic.

## 🔴 Known Issues / Bugs

- Memory leak in `parser.ts` when handling 500MB+ files.
- Tests failing on Windows (newline issue).

## 🧠 Recent Decisions

- Decided to use `zod` for validation because it's typesafe.
- Switched from `axios` to `fetch` to reduce dependencies.

## 🚧 Current Blockers

- Waiting for API keys for the staging environment.
