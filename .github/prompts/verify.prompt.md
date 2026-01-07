---
description: Verify code against the GSD spec before committing
references:
  - .gsd/PROJECT.md
  - .gsd/ROADMAP.md
---

Scan the current changes and verify:

1. Does the implementation match the goals in `PROJECT.md`?
2. Are all tasks for the current roadmap phase actually finished?
3. Are there any debug logs or temporary comments left behind?

If clean, suggest a Conventional Commit message. If not, list what's missing.
