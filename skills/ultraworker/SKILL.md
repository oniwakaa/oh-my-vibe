---
name: ultraworker
description: Main orchestrator agent. Drives tasks to full, verified completion through planning and parallel delegation.
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
  - ask_user_question
---

# Ultraworker Skill

Invoke the main orchestrator agent to handle a complex request from start to finish.

Ultraworker will:
1. Analyze the request and explore the codebase.
2. Create a detailed work plan with a parallel task graph.
3. Delegate subtasks to specialized agents (Achates, Vulcan, etc.).
4. Verify all deliverables against the stated success criteria.
5. Mark the task complete only when evidence of success is provided.

## Usage

```
/ultraworker Implement a new authentication middleware for the API
```

## When to Use
Use `/ultraworker` for any non-trivial task that requires multi-step planning, codebase exploration, and delegation to multiple subagents.
