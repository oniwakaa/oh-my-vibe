---
name: git-master
description: "MUST USE for ANY git operations. Atomic commits, rebase/squash, history search (blame, bisect, log -S). STRONGLY RECOMMENDED: Use with task(category='quick', load_skills=['git-master'], ...) to save context. Triggers: 'commit', 'rebase', 'squash', 'who wrote', 'when was X added', 'find the commit that'."
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
  - ask_user_question
---

# Git Master Skill

Expert git operations: atomic commits, rebase/squash, history search, and surgical git workflows.

## When to Use

Use `/git-master` when you need to perform any git operation, especially:
- Creating atomic commits with precise file staging
- Interactive rebase and squash operations
- Searching git history (blame, bisect, log -S)
- Finding which commit introduced a change
- Resolving merge conflicts
- Cherry-picking commits
- Managing branches

## Commit Workflow

### Atomic Commits

1. **Stage precisely**: Use `git add -p` or `git add <specific-files>` to stage only the changes that belong together.
2. **Write clear messages**: Follow the conventional commit format:
   ```
   <type>(<scope>): <subject>

   <body>

   <footer>
   ```
   Types: feat, fix, docs, style, refactor, perf, test, chore, ci

3. **One logical change per commit**: Each commit should represent one atomic, reviewable change.

### Atomic Commit Checklist

Before committing, verify:
- [ ] All changed files are related to ONE logical change
- [ ] Tests pass for this specific change
- [ ] Commit subject is under 50 characters
- [ ] Commit subject uses imperative mood ("add" not "added")
- [ ] Body explains WHY (context), not HOW (implementation)
- [ ] No commented-out code
- [ ] No debug prints or console.logs

### Commit Body Template

For non-trivial changes, use this body structure:

```
feat(auth): add JWT token validation

- Add validateJwt() function with RS256 support
- Integrate token validation in auth middleware
- Add environment variable for JWT_SECRET

Why: Previous auth used session cookies which don't scale
     for API-first microservices architecture.

Breaking: Session-based auth endpoints removed.
Migration: Clients must use /auth/token endpoint.
```

### Interactive Staging

```bash
# Stage specific hunks
git add -p

# For each hunk, answer:
# y = stage this hunk
# n = skip this hunk
# s = split into smaller hunks
# q = quit
```

### Example: Atomic Commits for a Feature

```bash
# Commit 1: Database schema
git add db/migrations/001_add_users_table.sql
git commit -m "feat(db): add users table schema"

# Commit 2: Model layer
git add src/models/user.ts
git commit -m "feat(models): add User model with password hashing"

# Commit 3: API layer
git add src/api/users.ts
git commit -m "feat(api): add user registration endpoint"

# Commit 4: Tests
git add tests/api/users.test.ts
git commit -m "test(api): add registration endpoint tests"
```

### Rebase/Squash

- Use `git rebase -i` for interactive rebase.
- Always rebase onto the target branch, not merge.
- Squash only related commits; never squash unrelated changes.
- When rebasing, resolve conflicts per-commit, not all at once.

## History Search

### Find When Something Was Added

```bash
git log -S "search_string" --oneline
git log -S "search_string" --source --all
```

### Find Who Wrote a Line

```bash
git blame -L 10,20 <file>
git blame -w <file>  # ignore whitespace
```

### Find the Commit That Introduced a Bug

```bash
git bisect start
git bisect bad          # current commit is bad
git bisect good <hash>  # known good commit
# Follow prompts until bisect finds the culprit
git bisect reset
```

### Search Commit Messages

```bash
git log --grep="pattern" --oneline
git log --author="name" --oneline
git log --since="2024-01-01" --until="2024-12-31" --oneline
```

## Quick Reference

| Task | Command |
|------|---------|
| Stage specific files | `git add <files>` |
| Stage hunks | `git add -p` |
| Commit all staged | `git commit -m "message"` |
| Amend last commit | `git commit --amend` |
| Interactive rebase | `git rebase -i HEAD~N` |
| Squash last N commits | `git rebase -i HEAD~N` then mark as squash |
| Cherry-pick | `git cherry-pick <hash>` |
| Find commit by content | `git log -S "text" --oneline` |
| Blame a line range | `git blame -L 10,20 <file>` |
| Bisect a bug | `git bisect start/good/bad/reset` |
| Stash changes | `git stash` / `git stash pop` |
| List branches | `git branch -a` |
| Delete branch | `git branch -d <name>` |