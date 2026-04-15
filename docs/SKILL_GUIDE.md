---
name: skills
description: Skill discovery matrix and usage guide for oh-my-vibe
license: MIT
compatibility: Python 3.12+
user-invocable: false
allowed-tools:
  - read_file
  - grep
  - ask_user_question
---

# Skill Discovery Guide

## How Skills Work

Skills are slash commands that invoke specialized workflows. Type `/` in Vibe CLI to see available skills.

## Skill Matrix by Task

| Task | Primary Skill | Supporting Skills |
|------|---------------|-------------------|
| Build a new feature | `/ultrawork` | `/interview-me` (planning), `/review-work` (verification) |
| Fix a bug | `/ultrawork` | `/tdd-gate` (if complex), `/git-master` (commit) |
| Refactor code | `/vulcan` | `/review-work` (after), `/ai-slop-remover` |
| Understand codebase | `/minerva` | Agrippa/Varro (background) |
| Plan architecture | `/interview-me` → `/plan` | `/censor` (gap check), `/cato` (approval) |
| Review PR | `/review-work` | `/git-master` (history) |
| Add tests | `/tdd-gate` | `/ultrawork` (if with feature) |
| Browser testing | `/playwright` | `/dev-browser` (persistent state) |
| Create commit | `/git-master` | None |
| Deep work, hands-off | `/vulcan` | None |

## Orchestration Workflows

### Full Feature Development
```
/interview-me I want to add X
[censor reviews plan for gaps]
[cato approves/rejects plan]
/start-work
[Fabius executes plan via subagents]
/review-work
[verification swarm runs]
/git-master commit
```

### Bug Fix with TDD
```
/tdd-gate Fix the race condition in session manager
[RED: write failing test]
[GREEN: implement minimum fix]
[REFACTOR: clean up]
/review-work
/git-master commit
```

### Exploration Only
```
/minerva How does the authentication middleware work?
[Minerva reads, analyzes, explains — no edits]
```

## Skill Chaining

Skills can be chained for complex workflows:
- `/ultrawork` internally chains: intent-gate → exploration → planning → delegation → verification
- `/review-work` internally spawns: Oracle(goal) + Oracle(quality) + Oracle(security) + QA + Context miner
