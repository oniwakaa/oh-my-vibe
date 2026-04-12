---
name: ulw
description: Short alias for /ultrawork. Invokes Hercules in full-automatic mode — intent gate, plan, delegate, verify, complete.
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

# ULW — Ultrawork Alias

This is a short alias for `/ultrawork`. Hercules will:

1. Classify your intent.
2. Explore the codebase.
3. Plan via todo list.
4. Delegate to specialists in parallel.
5. Verify and report completion.

## Usage

```
/ulw <your goal>
```

Equivalent to `/ultrawork <your goal>`. Use whichever you prefer.
