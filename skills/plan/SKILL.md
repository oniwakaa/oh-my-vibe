---
name: plan
description: Alias for Janus planning mode. Activates Janus to produce a structured implementation plan for a stated goal.
license: MIT
compatibility: Python 3.12+
user-invocable: true
allowed-tools:
  - read_file
  - write_file
  - bash
  - grep
  - todo
  - ask_user_question
---

# Plan Skill

A direct alias for Janus planning mode. Use `/plan` when you know what you
want to build and want a structured plan before implementation begins.

## Difference from `/interview-me`

- `/interview-me` — Janus interviews you first (2–5 questions) before planning.
  Use when the goal has open ambiguities.
- `/plan` — Janus goes directly to planning with minimal questions.
  Use when the goal is already well-defined.

## What Janus Produces

A structured Markdown plan saved to `.vibe/plan-<slug>.md` containing:
- **Goal** — What success looks like.
- **Constraints** — Hard boundaries the implementation must respect.
- **Tasks** — File-level, checkable task list.
- **Acceptance Criteria** — Exact, verifiable conditions.
- **Verification Commands** — Commands to run to confirm completion.

## Usage

```
/plan <describe your goal>
```

Example:

```
/plan Add pagination to the /users endpoint using cursor-based pagination
```

## After Planning

- Review the plan in `.vibe/plan-<slug>.md`.
- Run `/start-work` to hand it off to Fabius.
- Or run `/censor` / `/cato` to validate the plan first.
