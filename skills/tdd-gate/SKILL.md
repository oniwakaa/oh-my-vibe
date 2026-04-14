---
name: tdd-gate
description: Enforces a strict RED -> GREEN -> REFACTOR workflow for non-trivial implementation tasks.
license: MIT
compatibility: Python 3.12+
user-invocable: true
allowed-tools:
  - write_file
  - bash
  - read_file
  - search_replace
---

# TDD Gate

The `/tdd-gate` command transforms the implementation process into a rigorous engineering discipline. It prevents the "code first, test later" anti-pattern.

The agent must follow these exact phases in order:

1. **RED Phase**:
   - Identify the expected behavior.
   - Write a failing test case that precisely targets the new functionality.
   - Run the test and **confirm it fails** with the laziest possible implementation (or no implementation at all).
   - Evidence required: Output showing the test failure.

2. **GREEN Phase**:
   - Write the *minimum amount of code* necessary to make the test pass.
   - Run the test and **confirm it passes**.
   - Evidence required: Output showing the test passage.

3. **REFACTOR Phase**:
   - Clean up the implementation, remove redundancies, and ensure the code follows the codebase style.
   - Run the test again and **confirm it still passes**.
   - Evidence required: Output showing the test still passes after refactoring.

## Usage

```
/tdd-gate Implement the user password reset logic
```

## When to Use
- For any logic-heavy task where the cost of a bug is high.
- When implementing critical infrastructure or security-related features.
- When the user specifically asks for a "test-driven" approach.

## Success Criteria
The feature is considered complete only when there is a documented transition from RED to GREEN to REFACTOR, with terminal output proving each state.
