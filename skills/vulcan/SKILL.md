---
name: vulcan
description: Deep autonomous worker for independent goal execution.
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

Switch to the Vulcan agent profile (`~/.vibe/agents/vulcan.toml`) for this session.
Then adopt the Vulcan persona and execute the user's request. Give a goal; Vulcan forges the solution independently.
