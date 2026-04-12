---
name: init-deep
description: Generate a hierarchical AGENTS.md file tree for the current project. Creates a root AGENTS.md and per-directory AGENTS.md files tailored to each module.
license: MIT
compatibility: Python 3.12+
user-invocable: true
allowed-tools:
  - read_file
  - write_file
  - bash
  - grep
  - todo
---

# Init-Deep Skill

Generate a full AGENTS.md hierarchy for the current project so that any Vibe CLI
agent can understand the codebase structure, conventions, and module boundaries
without re-exploring from scratch every session.

## What This Skill Produces

1. **Root `AGENTS.md`** — Project-wide context: goal, tech stack, top-level
   directory map, coding conventions, test commands, CI/CD overview.

2. **Module-level `AGENTS.md` files** — One per significant subdirectory
   (e.g., `src/`, `src/api/`, `src/db/`, `tests/`). Each covers: the module's
   purpose, key files, internal conventions, and any gotchas specific to that area.

## Workflow

When invoked, the agent will:

1. Agrippa the project tree with grep and bash to identify all significant directories.
2. Read representative files from each directory to understand its purpose and conventions.
3. Write a root `AGENTS.md` at the project root.
4. Write per-directory `AGENTS.md` files in each significant subdirectory.
5. Present a summary of what was generated.

## Usage

```
/init-deep
```

Run this once when setting up oh-my-vibe on a new project. Re-run it after major
structural refactors to keep the context files current.

## Notes

- Existing `AGENTS.md` files will be read but not overwritten unless you confirm.
- The generated files are plain Markdown — edit them freely to add project-specific
  context that the agent cannot infer from the code.
