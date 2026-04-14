---
name: dev-browser
description: "Browser automation with persistent page state. Use when users ask to navigate websites, fill forms, take screenshots, extract web data, test web apps, or automate browser workflows. Trigger phrases include 'go to [url]', 'click on', 'fill out the form', 'take a screenshot', 'scrape', 'automate', 'test the website', 'log into', or any browser interaction request."
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

# Dev Browser Skill

Browser automation that maintains page state across script executions. Write small, focused scripts to accomplish tasks incrementally. Once you've proven out part of a workflow and there is repeated work to be done, you can write a script to do the repeated work in a single execution.

## Choosing Your Approach

- **Local/source-available sites**: Read the source code first to write selectors directly
- **Unknown page layouts**: Use accessibility snapshots to discover elements
- **Visual feedback**: Take screenshots to see what the user sees

## Setup

**Standalone Mode (Default):**

```bash
npx @anthropic-ai/dev-browser@latest
```

Add `--headless` flag if user requests it. Wait for the `Ready` message before running scripts.

## Key Principles

1. **Start the browser first** — ensure dev-browser is running before executing any automation.
2. **Navigate first** — always navigate to the target URL before interacting.
3. **Snapshot before interacting** — get the page state before clicking or filling.
4. **Re-snapshot after navigation** — significant DOM changes require a fresh snapshot.
5. **Close when done** — free browser resources when automation is complete.

## Common Workflows

### Navigation and Screenshot

```
1. Navigate to URL
2. Wait for page load
3. Take screenshot for visual verification
4. Extract text or data as needed
```

### Form Filling

```
1. Navigate to form page
2. Snapshot to discover form elements
3. Fill each field using element references
4. Submit form
5. Verify result page
```

### Web Scraping

```
1. Navigate to target page
2. Extract structured data from the page
3. Write extracted data to file or return as structured output
```

## Anti-Patterns

- Never hardcode selectors without checking the page first
- Never assume a page has finished loading — always wait
- Never skip the snapshot step before interacting
- Never leave browser sessions open when done