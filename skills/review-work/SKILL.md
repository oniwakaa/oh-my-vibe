---
name: review-work
description: Post-implementation review orchestrator. Launches a parallel swarm of specialists to verify goal alignment, code quality, security, and functional correctness.
license: MIT
compatibility: Python 3.12+
user-invocable: true
allowed-tools:
  - read_file
  - grep
  - todo
  - task
  - bash
---

# Review Work Skill

The `/review-work` command is the final quality gate. It prevents "it should work" syndrome by mandating a multi-perspective verification of the implementation before a task is marked complete.

When invoked, the orchestrator will launch a **Verification Swarm** in parallel:

1. **The Architect (Oracle)**: Verifies if the implementation satisfies the original Goal and all Constraints. Checks for architectural drift.
2. **The Code Reviewer (Oracle)**: Analyzes for code quality, adherence to existing codebase patterns, and maintainability.
3. **The Security Specialist (Oracle)**: Scans for common vulnerabilities, API key leaks, and security anti-patterns.
4. **The QA Lead (Deep/Unspecified-High)**: Executes manual verification tests, runs the build, and confirms the observable success criteria are met.
5. **The Context Miner (Deep/Unspecified-High)**: Checks for regressions in related modules and ensures no "collateral damage" was caused by the changes.

## Usage

```
/review-work
```

## When to Use
- Immediately after completing the implementation of a non-trivial feature or bug fix.
- Before marking a todo item as `completed`.
- Before creating a Pull Request.
- When the user requests "Check my work" or "Verify this implementation".

## Success Criteria
The work is considered "Verified" only when all members of the swarm return a **PASS**. Any **FAIL** must be resolved before the task is closed.
