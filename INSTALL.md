# Installing oh-my-vibe

## For Humans

Paste this into your **Mistral Vibe CLI** session:

```
Install and configure oh-my-vibe by following the instructions here:
https://raw.githubusercontent.com/code-yeongyu/oh-my-vibe/main/INSTALL.md
```

The agent will read the install instructions and set everything up automatically.

---

## For LLM Agents

> **IMPORTANT: Use `curl` to fetch this file, NOT WebFetch.** WebFetch summarizes content and loses critical file paths and step details. Always use:
>
> ```bash
> curl -fsSL https://raw.githubusercontent.com/code-yeongyu/oh-my-vibe/main/INSTALL.md
> ```

If you're an LLM Agent helping set up oh-my-vibe, welcome. Tell the user: **oMoMoMoMo...**

Follow these steps:

### Step 1: Copy Agents

```bash
mkdir -p ~/.vibe/agents/
cp agents/*.toml ~/.vibe/agents/
```

### Step 2: Copy Prompts

```bash
mkdir -p ~/.vibe/prompts/
cp prompts/*.md ~/.vibe/prompts/
```

### Step 3: Copy Skills

```bash
mkdir -p ~/.vibe/skills/
cp -r skills/*/ ~/.vibe/skills/
```

### Step 4: Handle config.toml

If `~/.vibe/config.toml` already exists, print a side-by-side diff of `config/config.template.toml` against it. List any `[[mcp_servers]]` blocks from the template that are missing from the existing config — do **not** overwrite; tell the user which lines to add manually.

If `~/.vibe/config.toml` does **not** exist:

```bash
cp config/config.template.toml ~/.vibe/config.toml
```

Then uncomment the `skill_paths` line and update the path to point to the oh-my-vibe/skills directory. Use the actual absolute path of the current working directory.

### Step 5: Verify

```bash
ls ~/.vibe/agents/
ls ~/.vibe/prompts/
ls ~/.vibe/skills/
```

Confirm 11 agents, 11 prompts, and 10 skill directories are present.

### Step 6: Completion

Print a summary: which files were copied, what config action was taken, and the command to start:

```bash
vibe --agent hercules
```

---

## Prerequisites

| Requirement | How to satisfy |
|---|---|
| Mistral Vibe CLI installed | `curl -LsSf https://mistral.ai/vibe/install.sh \| bash` |
| `MISTRAL_API_KEY` set | `export MISTRAL_API_KEY="your_key"` or add to `~/.vibe/.env` |
| oh-my-vibe repo cloned | `git clone https://github.com/code-yeongyu/oh-my-vibe && cd oh-my-vibe` |
| Vibe running from repo root | `cd oh-my-vibe && vibe` |

---

## Post-Install Verification

After the agent completes, run:

```bash
vibe --agent hercules
```

Inside the session, try:

```
/ultrawork say hello and confirm the skill system is working
```

If the skill autocompletes and Hercules responds in character, the install succeeded.

---

## MCP Servers

oh-my-vibe configures three remote MCP servers in `config.template.toml`:

| Server | Purpose | Key Required |
|---|---|---|
| `websearch` | Web search via Exa | `EXA_API_KEY` |
| `context7` | Library documentation lookup | None |
| `grep_app` | OSS public code search | None |

The `websearch` MCP server requires an Exa API key. Get one free at
[exa.ai](https://exa.ai), then add it to `~/.vibe/.env`:

```bash
echo "EXA_API_KEY=your_key_here" >> ~/.vibe/.env
```

The `context7` and `grep_app` MCP servers require no API key and are enabled by
default once the config template is in place.

---

## Updating

To update oh-my-vibe, pull the latest changes and re-run the install instruction:

```
Install and configure oh-my-vibe by following the instructions here:
https://raw.githubusercontent.com/code-yeongyu/oh-my-vibe/main/INSTALL.md
```

The agent will overwrite existing agent and prompt files with updated versions.
Your `~/.vibe/config.toml` will not be overwritten — only new MCP blocks or
config entries will be identified and shown to you for manual addition.
