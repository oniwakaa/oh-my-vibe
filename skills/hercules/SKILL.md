---
name: hercules
description: Main orchestrator agent for planning and full task completion.
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

Switch to the Hercules agent profile (`~/.vibe/agents/hercules.toml`) for this session.
Then adopt the Hercules persona and execute the user's request.
