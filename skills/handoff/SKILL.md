---
name: handoff
description: Create a detailed context summary for continuing work in a new session.
license: MIT
compatibility: Python 3.12+
user-invocable: true
allowed-tools:
  - read_file
  - grep
  - todo
  - bash
---

# Handoff Skill

The `/handoff` command is used when a session is reaching its limit or when transitioning work between different agents/sessions. It ensures that no critical context, decision, or pending task is lost.

The agent will synthesize the current state into a structured **Handoff Document** including:

1. **Current Status**: What has been achieved so far.
2. **Completed Work**: A summary of files modified and the logic changes implemented.
3. **Pending Todos**: The exact state of the todo list, including items `in_progress` and `pending`.
4. **Key Decisions**: Architectural choices made, trade-offs accepted, and the reasoning behind them.
5. **Blocking Issues**: Any unresolved bugs, missing information, or external dependencies.
6. **Immediate Next Steps**: The first 3-5 atomic actions the next agent must take to resume progress without friction.
7. **Context Map**: Relevant file paths, line numbers, and symbols that are central to the current work.

## Usage

```
/handoff
```

## When to Use
- Before ending a long session.
- When switching from an orchestrator (Hercules) to a specialized implementer (Vulcan) for a long-term task.
- When a task is too large for a single context window and needs to be broken across sessions.
- Before handing off to a human reviewer.

## Session Storage

Handoff documents should be stored for context continuity:

```
~/.vibe/sessions/
├── handoff-2026-01-15-auth-feature.md
├── handoff-2026-01-16-rate-limiter.md
└── handoff-2026-01-17-refactor-database.md
```

**Storage format:**

```markdown
# Handoff Document: [Feature Name]

**Date**: 2026-01-15
**Session ID**: ses_abc123
**Agent**: Hercules

## Current Status
[What has been achieved]

## Completed Work
- File: src/auth/jwt.ts (lines 42-67) — JWT validation logic
- File: tests/auth.test.ts (lines 15-30) — Test coverage added
- Decision: Use RS256 algorithm (ES256 failed in some environments)

## Pending Todos
- [ ] in_progress: Add token refresh logic
- [ ] pending: Update API documentation
- [ ] pending: Add integration tests

## Key Decisions
- Chose JWT over session cookies (API-first, stateless)
- Library: jsonwebtoken (most maintained)
- Token expiry: 15 minutes (configurable)

## Blocking Issues
- Need DevOps approval for new environment variable (JWT_SECRET)
- Redis not available in staging (token blacklisting blocked)

## Immediate Next Steps
1. Add JWT_SECRET to staging environment variables
2. Implement token refresh in src/auth/refresh.ts
3. Write integration tests for refresh flow

## Context Map
- Key files:
  - src/auth/jwt.ts:42-67 (validation logic)
  - src/middleware/auth.ts:15-30 (middleware integration)
  - tests/auth.test.ts:15-30 (test coverage)
- Related modules: user-service, rate-limiter (shared context)
```

## Resuming from Handoff

When resuming:
```
/session [session-id]
/handoff
```

The agent reads the handoff document, checks pending todos, and continues from the immediate next steps.
