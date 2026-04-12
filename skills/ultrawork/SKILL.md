---
name: ultrawork
description: Full-automatic coding mode. Hercules classifies intent, builds a plan, delegates implementation, and verifies results — without interrupting you.
license: MIT
compatibility: Python 3.12+
user-invocable: true
allowed-tools:
  - read_file
  - write_file
  - bash
  - grep
  - search_replace
  - todo
  - task
  - ask_user_question
---

# Ultrawork Skill

Invoke Hercules in full-automatic discipline mode. Hercules will:

1. Classify your intent (implement / research / plan / review / search / vision).
2. Agrippa the codebase to understand the relevant area.
3. Produce a task list in the todo panel.
4. Delegate work to the appropriate specialist subagents in parallel.
5. Integrate results, verify correctness, and mark the task complete.

## When to Use

Use `/ultrawork` (or `/ulw`) when you have a clear goal and want the system to handle
the full implementation loop without further prompting.

## What to Provide

State your goal in a single message. The more specific you are, the fewer questions
Hercules will ask. Examples:

- `/ultrawork Add a retry mechanism with exponential backoff to the HTTP client`
- `/ulw Refactor the auth module to use environment variables instead of hardcoded values`
- `/ultrawork Fix the race condition in the session manager reported in issue #42`

## Hercules Will

- Ask at most one clarifying question if the goal is ambiguous in a way that
  prevents safe implementation.
- Create and manage the todo list (Ctrl+T to view).
- Spawn subagents for parallel work without user interaction.
- Report completion with a summary of what was changed and what was verified.

## Hercules Will Not

- Expand scope beyond the stated goal.
- Make irreversible changes without confirming them if they affect files outside the
  stated area.
- Mark complete without running at least one verification step (test run, command
  output, or file diff review).
