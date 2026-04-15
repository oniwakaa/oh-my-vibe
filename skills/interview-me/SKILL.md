---
name: interview-me
description: Janus interview mode. Janus explores the codebase, asks you targeted questions to close ambiguities, and produces a decision-complete plan.
license: MIT
compatibility: Python 3.12+
user-invocable: true
allowed-tools:
  - read_file
  - write_file
  - bash
  - grep
  - todo
  - ask_user_question
---

# Interview-Me Skill

Activate Janus in interview mode. Janus will agrippa the relevant parts
of your codebase, then ask you a focused set of questions to close ambiguities
before producing a decision-complete implementation plan.

## What Janus Does

1. **Agrippas first.** Reads relevant files and code so it does not ask you things
   it can discover by looking.

2. **Interviews.** Asks 2–5 targeted questions using the interactive question UI.
   Each question is framed with the decision it unlocks.

3. **Plans.** Writes a structured plan to `.vibe/plan-<slug>.md`.

4. **Presents.** Shows you where the plan was saved and offers to revise any section.

## Usage

```
/interview-me <describe your goal>
```

Example:

```
/interview-me I want to add rate limiting to the API gateway
```

## Interview Workflow Examples

### Example 1: Feature Planning
```
/interview-me I want to add real-time notifications to my app

Janus will ask:
1. What's the primary notification channel? (WebSocket, SSE, polling)
2. Who receives notifications? (users, groups, tenant-scoped)
3. What's the expected message volume?
4. Do you need persistence for offline users?
5. Should notifications be actionable in-app?
```

### Example 2: Architecture Decision
```
/interview-me Should I use GraphQL or REST for my API?

Janus will explore:
- Team experience with each
- Client requirements (mobile, web, third-party)
- Query complexity needs
- Caching strategies
- Real-time requirements
```

### Example 3: Database Migration
```
/interview-me I need to migrate from PostgreSQL to MongoDB

Janus will ask:
1. What's the primary driver? (scale, flexibility, cost)
2. How complex are your current relationships?
3. Do you need ACID transactions?
4. What's your data migration timeline?
5. Are there stored procedures to translate?
```

## After the Interview

Review the plan file, then run `/start-work` to hand it off to Fabius for execution.
Or run `/censor` for a gap analysis, or `/cato` for a reviewal before executing.

## Tips

- Give Janus a clear goal statement so it can agrippa the right area.
- The more context you provide upfront, the fewer questions Janus will need to ask.
- Janus will not start planning until the interview is complete.
