---
name: ralph-loop
description: Retry loop. Hercules keeps re-attempting the current task until it reaches 100% completion or hits an unresolvable blocker.
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

# Ralph-Loop Skill

Hercules retries the current task until it is 100% complete. Unlike `/ulw-loop`
(which progresses through multiple tasks), `/ralph-loop` focuses entirely on
the current task and does not move on until it is fully verified.

## When to Use

Use `/ralph-loop` when:
- A previous ultrawork pass produced incomplete or broken output.
- A specific test is failing and you want the agent to keep iterating until it passes.
- A task is conceptually straightforward but requires repeated attempts (e.g., fixing
  a flaky integration, aligning output format to a strict specification).

## Retry Strategy

On each pass, Hercules:
1. Reads the current state of the failing test / broken output.
2. Diagnoses the remaining gap.
3. Applies a targeted fix.
4. Runs verification.
5. If verification passes: marks complete and reports.
6. If verification fails: loops with updated diagnosis.

## Stopping Conditions

The loop stops when:
- Verification passes (task complete).
- Hercules has retried N times (default: 5) without progress — reports the blocker.
- An unresolvable external dependency is identified (missing credential, network
  resource, etc.).

## Usage

```
/ralph-loop
```

Or with context:

```
/ralph-loop The authentication test keeps failing with a 403 — keep trying until it passes
```
