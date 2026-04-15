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

## Verification Swarm Architecture

When invoked, the orchestrator launches **5 parallel subagents**:

| Agent | Category | Purpose | Pass Criteria |
|-------|----------|---------|----------------|
| Oracle (Goal) | unspecified-high | Verifies implementation satisfies original goal + constraints | All stated requirements met |
| Oracle (Quality) | unspecified-high | Code quality, patterns, maintainability | No major smells, follows conventions |
| Oracle (Security) | unspecified-high | Vulnerabilities, API key leaks, anti-patterns | No secrets, no SQL injection paths, no XSS vectors |
| QA Lead (Deep) | deep | Manual verification tests, build execution | Tests pass, build succeeds |
| Context Miner (Deep) | deep | Regressions in related modules | No unintended side effects |

## Output Format

The verification swarm produces structured output:

```
┌─────────────────────────────────────────────────────────────┐
│ VERIFICATION SWARM RESULTS                                  │
├─────────────────────────────────────────────────────────────┤
│ │ Verifier      │ Status │ Summary                         │
│ │───────────────│────────│─────────────────────────────────│
│ │ Goal (Oracle) │  ✓ PASS│ Goal met: rate limiter added   │
│ │ Quality       │  ✓ PASS│ Follows existing patterns      │
│ │ Security      │  ✓ PASS│ No secrets, no injection paths │
│ │ QA (Deep)     │  ✓ PASS│ Build passes, tests pass       │
│ │ Context       │  ✓ PASS│ No regressions in related code │
├─────────────────────────────────────────────────────────────┤
│ VERDICT: ✅ VERIFIED                                        │
│ Summary: Implementation complete. 5/5 verifiers passed.      │
│ Ready for commit. Use /git-master to create atomic commit. │
└─────────────────────────────────────────────────────────────┘
```

If any verifier fails:

```
│ │ Security      │  ✗ FAIL│ Found hardcoded API key in src/config.ts:42 │
├─────────────────────────────────────────────────────────────┤
│ VERDICT: ❌ VERIFICATION FAILED                             │
│ Required Actions:                                           │
│ 1. Remove hardcoded API key from src/config.ts:42          │
│ 2. Use environment variable instead                          │
│ Run /review-work again after fixes.                         │
└─────────────────────────────────────────────────────────────┘
```

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
The work is considered "Verified" only when all 5 verifiers return **PASS**. 
Any **FAIL** must be resolved before the task is closed.
