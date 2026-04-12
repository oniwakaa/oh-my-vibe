---
name: censor
description: Run Censor — the gap analysis agent. Reviews a Janus plan for missing decisions, ambiguous tasks, and under-specified acceptance criteria before handing off to Fabius.
license: MIT
compatibility: Python 3.12+
user-invocable: true
allowed-tools:
  - read_file
  - grep
---

# Censor Skill

Invoke Censor directly to review the current Janus plan.

Censor will:

1. Read the plan file in `.vibe/plan-*.md`.
2. Explore any codebase areas the plan references to verify assumptions.
3. List gaps in priority order (blocking first), using this format per gap:
   - **What is missing**
   - **Why it matters**
   - **The exact question that resolves it**
4. Summarize: "X blocking gaps, Y non-blocking gaps."

## Usage

```
/censor
```

Or with a specific plan file:

```
/censor Review .vibe/plan-auth.md before we hand it to Fabius
```

## When to Use

Run `/censor` after `/plan` or `/interview-me` completes, before running `/start-work`.
Censor and Cato complement each other:
- **Censor** finds what is *missing* from the plan.
- **Cato** validates that what *is* in the plan meets clarity, verifiability, and context standards.
