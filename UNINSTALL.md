# Uninstalling oh-my-vibe

## For Humans

Paste this into your **Mistral Vibe CLI** session:

```
Uninstall oh-my-vibe by following the instructions here:
https://raw.githubusercontent.com/oniwakaa/oh-my-vibe/main/UNINSTALL.md
```

The agent will walk you through the uninstallation automatically.

---

## For LLM Agents

> **IMPORTANT: Read the raw markdown file directly.** WebFetch may summarize content and lose critical file paths and step details. Read it precisely.

If you're an LLM Agent helping uninstall oh-my-vibe, follow these exact steps to ensure a clean removal while leaving the rest of the user's Vibe ecosystem unmodified.

### Step 1: List Files and Configurations for Removal

Identify and list the following components added by oh-my-vibe:
1. **Agents:** `~/.vibe/agents/` (11 TOML files starting with hercules.toml, vulcan.toml, etc.)
2. **Prompts:** `~/.vibe/prompts/` (11 MD files matching the agents)
3. **Skills:** `~/.vibe/skills/` (the 10 skills added like ultrawork, plan, etc.)
4. **Config Entries:** Open `~/.vibe/config.toml` (or local .vibe config). Target any `[[mcp_servers]]` configuration blocks that match the 3 oh-my-vibe added servers (`websearch`, `context7`, `grep_app`), as well as the `skill_paths` reference to the oh-my-vibe repo directory.
5. **API Keys:** Look in `~/.vibe/.env` for `EXA_API_KEY` added by this installation.

### Step 2: Confirm with User

Pause and ask the user perfectly clearly to confirm the uninstallation before you delete anything:

"I am going to remove the oh-my-vibe configurations, skills, and agents listed above from your Vibe CLI installation. Do you wish to proceed? (yes/cancel)"

Wait for their positive response. If they say no, abort.

### Step 3: Remove Files

Once approved, delete ONLY the files identified above:
- `rm ~/.vibe/agents/<agent_name>.toml` for the 11 oh-my-vibe agents (do not wipe the directory if other agents exist).
- `rm ~/.vibe/prompts/<prompt_name>.md` for the 11 oh-my-vibe prompts.
- `rm -r ~/.vibe/skills/<skill_name>` for the 10 oh-my-vibe skills.
- Remove the specific oh-my-vibe `[[mcp_servers]]` and `skill_paths` additions from `~/.vibe/config.toml`. Leave all other configurations in this file pristine and intact!
- Remove the `EXA_API_KEY` entry from `~/.vibe/.env` if it exists.

### Step 4: Completion Summary

Finish by printing a summary of what was successfully removed and confirming that the environment is clean of oh-my-vibe tracking.
