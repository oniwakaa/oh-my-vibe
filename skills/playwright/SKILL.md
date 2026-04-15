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

Browser automation for testing, verification, scraping, and interaction.

## Setup Verification

Before using Playwright, verify setup:

```bash
# Check Node.js is installed
node --version  # v18+ required

# Install Playwright MCP
npx @playwright/mcp@latest --help

# If you see help output, setup is complete
```

### Common Setup Issues

| Issue | Cause | Solution |
|-------|-------|----------|
| `npx: command not found` | Node.js not installed | Install Node.js 18+ |
| `EACCES` errors | Permission issues | Use `npx --yes @playwright/mcp@latest` |
| Browser not found | Playwright browsers missing | Run `npx playwright install chromium` |
| MCP connection failed | Config not loaded | Check `~/.vibe/config.toml` has MCP block |

### Config Setup

Add to `~/.vibe/config.toml`:

```toml
[[mcp_servers]]
name = "playwright"
transport = "stdio"
command = "npx"
args = ["@playwright/mcp@latest"]
```

## When to Use

- **Verification**: Take screenshots, check element visibility after UI changes
- **Testing**: Navigate, interact, assert — E2E testing
- **Scraping**: Extract data from rendered pages
- **Documentation**: Screenshots for PRs, README updates
- **Debugging**: Visual inspection of running applications

## Workflow

### Basic Navigation
```
1. Navigate to URL
2. Wait for page load (network idle)
3. Interact with elements
4. Take screenshot for evidence
5. Extract needed data
```

### Verification Workflow
```
1. Navigate to app
2. Perform action (click, fill, submit)
3. Wait for result
4. Take "after" screenshot
5. Verify expected state
```

## Key Principles

1. **Always wait for page load** before interacting
   - Wait for `networkidle` or specific element
   
2. **Take before/after screenshots** for evidence
   - Document the impact of changes
   
3. **Handle authentication interactively**
   - Use `ask_user_question` if login required
   - Don't hardcode credentials
   
4. **Clean up resources**
   - Close browser tabs when done
   - Don't leave browsers open across sessions

## Troubleshooting

### "Browser context not found"
- The MCP server was restarted
- Navigate to the page again

### "Element not found"
- Page may not have loaded
- Add explicit wait: `await page.waitForSelector('[data-testid="element"]')`

### "Timeout waiting for navigation"
- Navigation didn't complete in time
- Increase timeout or check for errors

### Screenshots are blank
- Page didn't finish loading
- Add wait before screenshot

## Available Operations

Through the Playwright MCP:
- `browser_navigate` — Go to URL
- `browser_click` — Click element
- `browser_fill` — Fill input
- `browser_screenshot` — Capture page
- `browser_evaluate` — Run JavaScript
- `browser_wait` — Wait for condition
