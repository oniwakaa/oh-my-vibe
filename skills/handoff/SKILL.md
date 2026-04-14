---
name: handoff
description: Create a detailed context summary for continuing work in a new session.
license: MIT
compatibility: Python 3.12+
user-invocable: true
allowed-tools:
  - read_file
  - grep
  - todo
  - bash
---

# Handoff Skill

The `/handoff` command is used when a session is reaching its limit or when transitioning work between different agents/sessions. It ensures that no critical context, decision, or pending task is lost.

The agent will synthesize the current state into a structured **Handoff Document** including:

1. **Current Status**: What has been achieved so far.
2. **Completed Work**: A summary of files modified and the logic changes implemented.
3. **Pending Todos**: The exact state of the todo list, including items `in_progress` and `pending`.
4. **Key Decisions**: Architectural choices made, trade-offs accepted, and the reasoning behind them.
5. **Blocking Issues**: Any unresolved bugs, missing information, or external dependencies.
6. **Immediate Next Steps**: The first 3-5 atomic actions the next agent must take to resume progress without friction.
7. **Context Map**: Relevant file paths, line numbers, and symbols that are central to the current work.

## Usage

```
/handoff
```

## When to Use
- Before ending a long session.
- When switching from an orchestrator (Hercules) to a specialized implementer (Vulcan) for a long-term task.
- When a task is too large for a single context window and needs to be broken across sessions.
- Before handing off to a human reviewer.
