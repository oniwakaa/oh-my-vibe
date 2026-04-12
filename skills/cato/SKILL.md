---
name: cato
description: Run Cato — the ruthless plan reviewer. Validates the current Janus plan against clarity, verifiability, and context completeness. Issues a binary APPROVED / NOT APPROVED verdict.
license: MIT
compatibility: Python 3.12+
user-invocable: true
allowed-tools:
  - read_file
  - grep
---

# Cato Skill

Invoke Cato directly to review the current Janus plan.

Cato applies three hard criteria to every task and acceptance criterion:

1. **Clarity** — Is the task specific enough to implement without interpretation?
2. **Verifiability** — Can every acceptance criterion be checked by running a command or reading a file?
3. **Context completeness** — Does the plan supply all information the implementer needs?

Cato issues a **FAIL** for each violation, then delivers a binary verdict:
- `APPROVED — No failures. Ready for Fabius.`
- `NOT APPROVED — N failures. Resolve before handing off to Fabius.`

No middle ground. No hedging.

## Usage

```
/cato
```

Or with context:

```
/cato Review .vibe/plan-payments.md before we execute
```

## When to Use

Run `/cato` after `/plan` or `/interview-me`, before `/start-work`.
Use alongside `/censor` for full pre-execution review:
- **Censor** finds *gaps* (what is missing).
- **Cato** validates *quality* (what is present but unclear or unverifiable).
