---
name: ulw-loop
description: Continuous ultrawork loop. Hercules runs ultrawork passes repeatedly until you explicitly stop the loop or the todo list is empty.
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

# ULW-Loop Skill

Run Hercules in a continuous ultrawork loop. Each pass:

1. Checks the todo list for remaining items.
2. Executes the next batch of work.
3. Verifies and marks completed items.
4. Loops until the todo list is empty or you stop the session.

## When to Use

Use `/ulw-loop` when you have a large body of work that spans multiple ultrawork
cycles — for example, migrating a large codebase, implementing a multi-feature
sprint, or working through a long todo list without interrupting yourself.

## Usage

```
/ulw-loop <optional: initial goal or context>
```

## Stopping the Loop

The loop stops automatically when:
- The todo list is empty.
- Hercules encounters a blocker it cannot resolve.
- Hercules needs user confirmation before proceeding (scope expansion, risky change).

To stop manually, interrupt the session (Ctrl+C) or send a new message.

## Caution

The loop runs continuously and may consume significant API tokens on large tasks.
Monitor usage via your Mistral console if cost is a concern.
