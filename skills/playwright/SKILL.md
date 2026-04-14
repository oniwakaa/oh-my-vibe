---
name: playwright
description: "MUST USE for any browser-related tasks. Browser automation via Playwright MCP — verification, browsing, information gathering, web scraping, testing, screenshots, and all browser interactions."
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

# Playwright Browser Automation

This skill provides browser automation capabilities via the Playwright MCP server.

## When to Use

- Verifying UI changes — take screenshots, check element visibility
- Web scraping — extract data from rendered pages
- Testing web applications — navigate, interact, assert
- Information gathering — browse documentation, check live sites
- Taking screenshots for review or documentation

## Setup

The Playwright MCP server must be configured in `~/.vibe/config.toml`:

```toml
[[mcp_servers]]
name = "playwright"
transport = "stdio"
command = "npx"
args = ["@playwright/mcp@latest"]
```

## Workflow

1. **Navigate**: Use the browser to go to the target URL.
2. **Interact**: Click buttons, fill forms, select options, take screenshots.
3. **Verify**: Check that the page shows the expected content.
4. **Report**: Return the verification result with evidence (screenshots, extracted text).

## Key Principles

- Always wait for page load before interacting with elements.
- Take screenshots before and after changes to document the impact.
- Use `ask_user_question` if browser authentication is needed.
- Clean up: close browser tabs when done to free resources.

## Available Browser Operations

Through the Playwright MCP, the following operations are available:
- Navigate to URLs
- Click elements
- Fill forms and input fields
- Select dropdown options
- Take screenshots
- Extract text content
- Wait for elements and navigation
- Handle dialogs and popups