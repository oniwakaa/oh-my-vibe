# Installing oh-my-vibe

Paste the prompt below into any **Mistral Vibe CLI** session (from inside the
oh-my-vibe repository directory). The agent will copy all files to the correct
locations, validate the installation, and report completion.

---

## One-Line Install Prompt

```
Read the INSTALL.md file in the current directory, then install oh-my-vibe by:
1. Copying every file in agents/ to ~/.vibe/agents/
2. Copying every file in prompts/ to ~/.vibe/prompts/
3. Copying every directory in skills/ to ~/.vibe/skills/ (preserving subdirectory structure)
4. If ~/.vibe/config.toml already exists, print a side-by-side diff of config/config.template.toml against it and list any [[mcp_servers]] blocks from the template that are missing from the existing config — do not overwrite; tell me which lines to add manually. If ~/.vibe/config.toml does not exist, copy config/config.template.toml to ~/.vibe/config.toml.
5. Verify the installation by listing ~/.vibe/agents/, ~/.vibe/prompts/, and ~/.vibe/skills/ and confirming that all expected files are present.
6. Print a completion summary: which files were copied, what config action was taken, and the command to start using Hercules (vibe --agent hercules).
```

---

## Prerequisites

| Requirement | How to satisfy |
|---|---|
| Mistral Vibe CLI installed | `curl -LsSf https://mistral.ai/vibe/install.sh \| bash` |
| `MISTRAL_API_KEY` set | `export MISTRAL_API_KEY="your_key"` or add to `~/.vibe/.env` |
| oh-my-vibe repo cloned | `git clone https://github.com/<your-fork>/oh-my-vibe && cd oh-my-vibe` |
| Vibe running from repo root | `cd oh-my-vibe && vibe` |

---

## What the Install Prompt Does

1. **Copies agents** — 11 `.toml` files to `~/.vibe/agents/`
2. **Copies prompts** — 11 `.md` files to `~/.vibe/prompts/`
3. **Copies skills** — 7 skill directories (each containing a `SKILL.md`) to `~/.vibe/skills/`
4. **Handles config** — Merges or creates `~/.vibe/config.toml` safely
5. **Verifies** — Lists installed files and confirms nothing is missing
6. **Reports** — Prints a summary and your first command

---

## Post-Install Verification

After the agent completes, run:

```bash
vibe --agent hercules
```

Inside the session, try:

```
/ultrawork Say hello and confirm the skill system is working
```

If the skill autocompletes and Hercules responds in character, the install succeeded.

---

## Optional: Websearch MCP

The `websearch` MCP server requires an Exa API key. Get one free at
[exa.ai](https://exa.ai), then add it:

```bash
echo "EXA_API_KEY=your_key_here" >> ~/.vibe/.env
```

The `context7` and `grep_app` MCP servers require no API key and are enabled by
default once the config template is in place.

---

## Updating

To update oh-my-vibe, pull the latest changes and re-run the install prompt.
The agent will overwrite existing agent and prompt files with the updated versions.
Your `~/.vibe/config.toml` will not be overwritten — only new MCP blocks will
be identified and shown to you for manual addition.
