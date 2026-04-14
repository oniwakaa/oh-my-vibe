---
name: remove-ai-slops
description: "Removes AI-generated code smells from ALL changed files in the current branch and critically reviews the results. For a single file, use /ai-slop-remover instead."
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
---

# Remove AI Slops — Branch-Wide Cleanup

This is the branch-wide version of `/ai-slop-remover`. It finds ALL files changed in the current branch (compared to main/master), then runs the AI slop removal process on each one, collecting results across all files.

## When to Use

Use `/remove-ai-slops` when:
- You want to clean up AI-generated artifacts across an entire feature branch
- Before creating a pull request
- After a large AI-assisted implementation pass
- When multiple files need slop review

For a single file, use `/ai-slop-remover` instead.

## Workflow

1. **Identify changed files**: Run `git diff --name-only main...HEAD` (or appropriate base branch) to find all files changed in this branch.

2. **Process each file**: For each changed file, apply the AI slop removal criteria:
   - **Obvious Comments**: Remove comments restating the code, trivial docstrings, section dividers, commented-out code, TODO without concrete plan, notes without explaining WHY
   - **Over-Defensive Code**: Remove null checks for guaranteed values, unnecessary try-except, `isinstance()` checks for typed parameters, default values for required params, backward-compat shims
   - **Spaghetti Nesting**: Refactor nested if-else chains to early returns / guard clauses

3. **Safety Rules**:
   - NEVER remove error handling for I/O, network, or file operations
   - NEVER simplify validation for user input or external data
   - NEVER change public API signatures
   - NEVER remove type hints
   - NEVER remove BDD test comments (#given, #when, #then)
   - When in doubt, DO NOT CHANGE

4. **Report**: After processing all files, produce a summary:
   - Total files processed
   - Total issues found vs fixed vs skipped (safety)
   - Per-file breakdown of changes made
   - Any files that need manual review

## Difference from /ai-slop-remover

- `/ai-slop-remover`: Operates on a SINGLE file. Use for targeted cleanup.
- `/remove-ai-slops`: Operates on ALL changed files in the branch. Use for branch-wide cleanup.

## Execution

The skill will:
1. Detect all changed files in the branch
2. Spawn parallel subagents for each file (or batch for large change sets)
3. Collect and consolidate results
4. Produce a final summary report

When finished, review the summary report carefully. Not all suggested changes should be applied blindly — use your judgment.