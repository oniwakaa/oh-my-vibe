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

The `/tdd-gate` command transforms the implementation process into a rigorous engineering discipline. It prevents the "code first, test later" anti-pattern by enforcing test-first development.

## Test Framework Auto-Detection

The agent must auto-detect the project's test framework before starting:

| Language | Detection File | Test Command |
|----------|----------------|--------------|
| Node.js/TypeScript | `package.json` → "jest", "vitest", "mocha" | `npm test` / `pnpm test` |
| Python | `pytest.ini`, `setup.cfg`, `pyproject.toml` | `pytest` / `python -m pytest` |
| Rust | `Cargo.toml` → [dev-dependencies] test crates | `cargo test` |
| Go | `*_test.go` files | `go test ./...` |
| Ruby | `Gemfile` → "rspec", "minitest" | `bundle exec rspec` / `rails test` |
| Java/Kotlin | `pom.xml` or `build.gradle` test deps | `mvn test` / `./gradlew test` |

## RED Phase

1. **Identify expected behavior** from the user's request.
2. **Auto-detect test framework** using table above.
3. **Write a failing test** that targets the new functionality precisely.
4. **Confirm RED**: Run test and capture failing output.
   
   ```
   [TDD-GATE] Detected test framework: pytest
   [TDD-GATE] Running: pytest tests/test_new_feature.py -v
   [TDD-GATE] Result: FAILED - AssertionError: Expected X, got Y
   [TDD-GATE] ✅ RED phase confirmed. Proceeding to GREEN.
   ```

## GREEN Phase

1. **Write minimum code** to make the test pass — no extra features.
2. **Confirm GREEN**: Run test and capture passing output.

   ```
   [TDD-GATE] Running: pytest tests/test_new_feature.py -v
   [TDD-GATE] Result: PASSED - 1 test passed
   [TDD-GATE] ✅ GREEN phase confirmed. Proceeding to REFACTOR.
   ```

## REFACTOR Phase

1. **Clean up implementation** — remove redundancies, improve names, follow style.
2. **Confirm STILL GREEN**: Run test and confirm it still passes.

   ```
   [TDD-GATE] Refactored: extracted helper function, improved naming
   [TDD-GATE] Running: pytest tests/test_new_feature.py -v
   [TDD-GATE] Result: PASSED - 1 test passed (after refactoring)
   [TDD-GATE] ✅ All phases complete. Feature verified via TDD.
   ```

## Usage

```
/tdd-gate Implement user authentication with JWT tokens
/tdd-gate Add pagination to the products endpoint
/tdd-gate Create a background job to process webhooks
```

## When to Use

- Logic-heavy features where bugs are costly
- Security-related implementations (auth, encryption, permissions)
- Core business logic that needs regression protection
- When the user explicitly requests TDD
- When implementing algorithms or data transformations

## Success Criteria

Feature is complete ONLY when:
- [ ] Test framework auto-detected correctly
- [ ] RED phase: Test fails with lazy/no implementation (output shown)
- [ ] GREEN phase: Test passes with minimum implementation (output shown)
- [ ] REFACTOR phase: Test still passes after cleanup (output shown)

## Anti-Patterns

❌ Writing implementation before test
❌ Skipping RED confirmation
❌ Adding features "while you're at it"
❌ Writing tests that always pass (mocking wrong thing)
❌ Refactoring before GREEN (broken tests are hard to refactor)
