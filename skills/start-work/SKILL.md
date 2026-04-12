---
name: start-work
description: Activate Fabius on the most recent Janus plan. Reads the latest plan file in .vibe/ and begins execution.
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

# Start-Work Skill

Hand off the most recent Janus plan to Fabius for execution.

## Preconditions

- A plan file must exist in `.vibe/plan-*.md` (created by Janus via `/plan`
  or `/interview-me`).
- The plan must have been reviewed and approved (manually or via `/cato` review).

## What Happens

1. Fabius locates the most recent `.vibe/plan-*.md` file.
2. Fabius reads the plan: goal, tasks, acceptance criteria, verification commands.
3. Fabius loads the task list into the todo panel.
4. Fabius dispatches subagents to execute the tasks in the correct order.
5. Fabius verifies results against acceptance criteria and reports completion.

## Usage

```
/start-work
```

If multiple plan files exist in `.vibe/`, Fabius will list them and ask you which one
to execute before beginning.

## Tips

- Run `/interview-me` or `/plan` first if no plan exists yet.
- Run Censor (`/censor`) or Cato (`/cato`) on the plan before starting if you
  want a gap analysis or review pass before implementation begins.
