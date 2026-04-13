# AGENTS.md — oh-my-vibe
<!-- Workspace context file for Mistral Vibe CLI (read at session start) -->
<!-- Target runtime: mistral-vibe (github.com/mistralai/mistral-vibe) -->

## Project Goal

oh-my-vibe is a community-installable agent and skill ecosystem for Mistral Vibe CLI.

Agent names are preserved faithfully from the source. No agent is collapsed, skipped,
or renamed in this phase. Capabilities are ported as-is; prompt style is adapted
for Devstral based on verified guidance (see Devstral Prompt Guidance section).

---

## Project Details

**Repository:** `github.com/oniwakaa/oh-my-vibe` (branch: dev)
**Target Runtime:** mistral-vibe
**Language:** TypeScript (~1600 source files), Bun runtime

### Agents (11 total, from `src/agents/`)

| Agent | Role | Prompt Style |
|---|---|---|
| **Hercules** | Main orchestrator; plans, delegates, drives tasks to completion with aggressive parallel execution | Claude-optimized (mechanics-driven, detailed checklists) |
| **Achates** | Lightweight subagent variant of Hercules for delegated tasks | Claude-optimized |
| **Vulcan** | GPT-native deep autonomous worker; goal-driven, no hand-holding | GPT-native (principle-driven, XML-tagged) |
| **Janus** | Strategic planner with interview mode; identifies scope and ambiguities before one line of code | Dual-prompt: Claude variant (~1100 lines, 7 files) and GPT variant (~300 lines, XML-tagged, 3 principles) |
| **Fabius** | Todo orchestrator and conductor; executes Janus plans, delegates to subagents | Dual-prompt: Claude and GPT |
| **Minerva** | Read-only high-IQ consultant for architecture decisions and complex debugging | GPT-preferred; Claude fallback |
| **Censor** | Gap analyzer; reviews Janus plans for what was missed | Claude-optimized |
| **Cato** | Ruthless reviewer; validates plans against clarity, verification, and context criteria | GPT-preferred (xhigh) |
| **Varro** | Documentation and OSS code search; stays current on APIs and best practices | Speed-focused utility |
| **Agrippa** | Fast codebase grep for pattern discovery | Speed-focused utility |
| **Argus** | Vision and screenshot analysis; reads images and UI state | Vision-capable |

### Category-Based Routing (from `src/tools/delegate-task/constants.ts`)

Hercules delegates tasks not by model name but by **category**. The category resolves
automatically to the right model at runtime:

| Category | Intent | Devstral Mapping |
|---|---|---|
| `visual-engineering` | Frontend and UI work | devstral-small (fast) or devstral-2 |
| `ultrabrain` | Deep reasoning, complex architecture | devstral-2 |
| `quick` | Fast utility tasks | devstral-small |
| `deep` | Broad coding tasks | devstral-2 |
| `unspecified-high` | General high-effort work | devstral-2 |

### Skills (from `src/features/builtin-skills/skills/`)

oh-my-vibe has a built-in skill system that extends agent behaviors via SKILL.md
files with YAML frontmatter. The following skill categories exist in source:

| Skill / Command | Purpose |
|---|---|
| `ultrawork` | Trigger Hercules full-auto mode: intent gate → plan → delegate → verify |
| `ulw` | Alias for `ultrawork` (separate skill file, same behavior) |
| `ulw-loop` | Continuous ultrawork loop (runs until explicitly stopped) |
| `init-deep` | Generate hierarchical AGENTS.md files across the project tree |
| `start-work` | Activate Fabius on the latest Janus plan |
| `ralph-loop` | Retry loop — continues until 100% done |
| `interview-me` | Janus interview mode entry point |
| `plan` | Alias for Janus planning mode |
| `censor` | Run Censor gap analysis on the current plan |
| `cato` | Run Cato review; issues APPROVED / NOT APPROVED verdict |

### MCP Servers (Three-Tier System)

**Tier 1 — Built-in (remote HTTP):**
- `websearch` — web search via Exa API
- `context7` — library documentation lookup
- `grep_app` — OSS code search across public repos

**Tier 2 — Project-level (`.mcp.json`):**
- Standard MCP JSON loaded from the Claude Code `.mcp.json` convention

**Tier 3 — Skill-embedded:**
- Each skill can declare its own MCP servers in SKILL.md YAML; managed per-session

**Critical porting note:** In Vibe CLI, MCP configuration is GLOBAL in `~/.vibe/config.toml`
under `[[mcp_servers]]`. Do NOT put MCP blocks inside individual agent TOML files.
Skills may reference MCPs but not re-configure them.

### Key Features to Port

| Feature | Source Location | Vibe Equivalent |
|---|---|---|
| IntentGate classifier | `src/hooks/` (chat.message) | System prompt section in Hercules prompt |
| Hashline edit (LINE#ID) | `src/tools/` | Native Vibe tools (search_replace) — no port needed |
| Background agents (tmux) | `src/features/tmux-subagent/` | Vibe `task` tool with `agent_type = "subagent"` |
| Lifecycle hooks (52 total) | `src/hooks/` | System prompt constraints + Vibe skill logic |
| Context compaction | `src/plugin/` | Vibe handles natively |
| Todo enforcer | `src/features/boulder-state/` | Vibe native todo list (Ctrl+T) |

---

## Target Platform — Mistral Vibe CLI

**Repository:** `github.com/mistralai/mistral-vibe`
**Language:** Python 3.12+, installed via `uv tool install mistral-vibe`
**Default model:** Devstral (devstral-2 or devstral-small)
**Config root:** `~/.vibe/` (global) or `.vibe/` (project-local, highest priority)

### File Layout Produced by This Project

```
oh-my-vibe/
├── AGENTS.md                          ← this file (project workspace context)
├── INSTALL.md                         ← one-line install prompt for users
├── README.md                          ← human-readable overview
├── config/
│   └── config.template.toml           ← annotated config.toml template (copy to ~/.vibe/)
├── agents/
│   ├── hercules.toml
│   ├── achates.toml
│   ├── vulcan.toml
│   ├── janus.toml
│   ├── fabius.toml
│   ├── minerva.toml
│   ├── censor.toml
│   ├── cato.toml
│   ├── varro.toml
│   ├── agrippa.toml
│   └── argus.toml
├── prompts/
│   ├── hercules.md
│   ├── achates.md
│   ├── vulcan.md
│   ├── janus.md
│   ├── fabius.md
│   ├── minerva.md
│   ├── censor.md
│   ├── cato.md
│   ├── varro.md
│   ├── agrippa.md
│   └── argus.md
└── skills/
    ├── ultrawork/
    │   └── SKILL.md
    ├── ulw/
    │   └── SKILL.md
    ├── ulw-loop/
    │   └── SKILL.md
    ├── init-deep/
    │   └── SKILL.md
    ├── start-work/
    │   └── SKILL.md
    ├── ralph-loop/
    │   └── SKILL.md
    ├── interview-me/
    │   └── SKILL.md
    ├── plan/
    │   └── SKILL.md
    ├── censor/
    │   └── SKILL.md
    └── cato/
        └── SKILL.md
```

### Vibe CLI Format Reference

#### Agent files — `~/.vibe/agents/<name>.toml`

```toml
display_name = "Hercules"
description  = "Main orchestrator. Plans, delegates, drives tasks to completion."
safety       = "neutral"           # "safe" | "neutral" | "destructive" | "yolo"
auto_approve = false
enabled_tools = ["read_file", "write_file", "bash", "grep", "search_replace", "todo", "task", "ask_user_question"]
agent_type   = "primary"           # "primary" | "subagent" — subagent = delegatable
system_prompt_id = "hercules"      # maps to ~/.vibe/prompts/hercules.md
```

**agent_type rules:**
- `"primary"` — selectable by user with `vibe --agent <name>`
- `"subagent"` — usable via the `task` tool for delegated parallel work; not user-facing

**safety levels:**
- `"safe"` — auto-approves read-only tools (grep, read_file)
- `"neutral"` — requires approval for writes and commands
- `"destructive"` — auto-approves writes
- `"yolo"` — auto-approves everything

#### Skill files — `~/.vibe/skills/<skill-name>/SKILL.md`

```markdown
---
name: ultrawork
description: Full-automatic coding mode. Hercules explores, plans, implements, and verifies without hand-holding.
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

# Ultrawork Skill

Invoke Hercules in full-automatic discipline mode...
(detailed workflow instructions follow in body)
```

**YAML frontmatter fields:**
- `name` — slug used in skill discovery and slash command registration
- `description` — shown in autocompletion
- `license` — e.g. MIT
- `compatibility` — Python version range
- `user-invocable: true` — registers `/ultrawork` as a slash command in the Vibe UI
- `allowed-tools` — list of Vibe native tool names this skill may use

Skills are discovered from (in priority order):
1. `skill_paths` entries in config.toml
2. `.agents/skills/` in project root (Agent Skills standard path)
3. `.vibe/skills/` in project root (trusted folders only)
4. `~/.vibe/skills/` global

#### System Prompt files — `~/.vibe/prompts/<name>.md`

Plain Markdown. The `system_prompt_id` in the agent TOML (without `.md` extension)
resolves to this file. Replaces the default `prompts/cli.md`.

#### Global config — `~/.vibe/config.toml`

```toml
# Active model (api model name from console.mistral.ai)
active_model = "devstral-2"

# System prompt (default; overridden per-agent via system_prompt_id)
system_prompt_id = "hercules"

# MCP servers — GLOBAL ONLY, not per-agent
[[mcp_servers]]
name      = "websearch"
transport = "http"
url       = "https://api.exa.ai/mcp"
api_key_env    = "EXA_API_KEY"
api_key_header = "x-api-key"
api_key_format = "{token}"

[[mcp_servers]]
name      = "context7"
transport = "streamable-http"
url       = "https://mcp.context7.com/mcp"

[[mcp_servers]]
name      = "grep_app"
transport = "streamable-http"
url       = "https://grep.app/mcp"
```

---

## Devstral Prompt Guidance

Devstral is Mistral's agentic model trained for software engineering tasks within
agentic scaffolds (e.g. OpenHands, Vibe CLI). It differs meaningfully from Claude
and GPT in how it processes system prompts.

### Verified Findings

1. **Devstral is principle-driven, not mechanics-driven.**
   - Claude prompts rely on detailed checklists, step-by-step procedures, and enforcement
     mechanisms (`>800 lines` for Hercules in source).
   - Devstral performs better with concise principles, XML-tagged structure, and explicit
     decision criteria — similar to GPT-5.4's behavior pattern.
   - Source evidence: the GPT prompt for Janus achieves the same result with ~300 lines
     (3 principles) that the Claude variant needs ~1,100 lines for.

2. **Use XML-style section delimiters.**
   - Wrap major prompt sections in `<ROLE>`, `<EFFICIENCY>`, `<FILE_SYSTEM_GUIDELINES>`,
     `<CODE_QUALITY>`, `<CONSTRAINTS>`, `<WORKFLOW>` tags.
   - Devstral parses these reliably across context window stretches.

3. **Think before acting.**
   - Instruct Devstral to perform exploration and analysis before implementation.
   - Example: "Before editing any file, state your intended change and the exact lines
     you will modify. Then execute."

4. **Low temperature for agentic tasks.**
   - Use temperature 0.0–0.15 for deterministic, accurate agentic behavior.
   - Vibe's default is suitable; do not increase unless creativity is explicitly needed.

5. **Avoid over-prompting.**
   - Avoid legacy Claude prompt mechanics; they are over-specified for
     Claude's compliance model. Extract the core intent and rewrite as principles.
   - Each agent prompt should be self-contained and under 400 lines.

6. **Explicit persona anchoring.**
   - Start every prompt with: `You are <AgentName>, a specialized coding agent within
     the oh-my-vibe multi-agent system running on Mistral Vibe CLI.`
   - This anchors tone, role, and scope reliably.

### Prompt Template (Devstral-optimized)

```markdown
You are <AgentName>, a specialized coding agent within the oh-my-vibe multi-agent
system running on Mistral Vibe CLI. Your model is Devstral.

<ROLE>
[1-3 sentences: primary objective and what this agent is responsible for]
</ROLE>

<CONSTRAINTS>
- [Hard boundary 1]
- [Hard boundary 2]
</CONSTRAINTS>

<WORKFLOW>
1. [First principle / step]
2. [Second principle / step]
3. [Third principle / step — keep to ≤5 total]
</WORKFLOW>

<EFFICIENCY>
- Combine related file reads into one operation.
- State your plan in one sentence before using any tool.
- Never re-read a file you read in the same turn.
</EFFICIENCY>

<CODE_QUALITY>
- Write code that matches the established style of the file being edited.
- Minimal diffs — do not refactor what you are not asked to change.
- No placeholder comments ("TODO", "...", "add logic here").
</CODE_QUALITY>
```

---

## Porting Principles

1. **Research drives every decision.** Do not assume behavior — verify against source
   and docs before writing anything.

2. **One prompt per agent, Devstral-optimized.** There is only one model family here
   (Mistral/Devstral), so there is no dual-prompt requirement. Write the prompt for
   Devstral using the guidance above.

3. **MCP config is global.** All `[[mcp_servers]]` blocks go in `config.template.toml`.
   Individual agent TOML files must NOT contain MCP config.

4. **Skills transfer with minimal changes.** Port all 10 skills. The SKILL.md format is
   compatible — adapt the body workflow prose for Devstral's principle-driven style.

5. **The install experience is LLM-driven.** No shell scripts. No manual file-copying.
   The user pastes one prompt into Vibe CLI; the agent reads INSTALL.md and executes
   the full setup: copies agents, prompts, skills, config template, and validates the
   result.

6. **Subagents via `task` tool.** Hercules delegates to other agents using Vibe's native
   `task` tool. Target agents must have `agent_type = "subagent"` in their TOML.
   Primary agents (user-selectable) use `agent_type = "primary"`.

7. **Preserve every agent.** Do not collapse Censor into Janus, Cato into Minerva,
   or Varro into Agrippa. Every agent in the source has a distinct role.

8. **Write INSTALL.md last.** After all target file paths are confirmed, write INSTALL.md
   with the exact one-line prompt users paste into Vibe CLI to trigger automated install.

---

## Build Order (for the implementing agent)

Execute in this exact sequence to avoid forward references:

1. `config/config.template.toml` — global config with all MCP servers and field comments
2. `prompts/*.md` — all 11 system prompts (Devstral-optimized)
3. `agents/*.toml` — all 11 agent TOML files (referencing prompts by system_prompt_id)
4. `skills/*/SKILL.md` — all 10 skills with frontmatter and Devstral-adapted body
5. `README.md` — project overview, quickstart, agent roster table
6. `INSTALL.md` — exact install prompt (written last, after all paths confirmed)

---

## Where to Look

| Task | File(s) |
|---|---|
| Add or modify an agent | `agents/<name>.toml` + `prompts/<name>.md` |
| Add a slash command | `skills/<name>/SKILL.md` with `user-invocable: true` |
| Add an MCP server | `config/config.template.toml` under `[[mcp_servers]]` |
| Change the default model | `config/config.template.toml` → `active_model` |
| Adjust tool permissions | `config/config.template.toml` → `[tools.<name>]` |
| Review agent configuration | `agents/` |
| Review skill configuration | `skills/` |
| Verify Vibe format | `github.com/mistralai/mistral-vibe` README |

---

## Anti-Patterns

- Never put `[[mcp_servers]]` inside an agent `.toml` file — it belongs in `config.toml` only.
- Never use `safety = "yolo"` for orchestrator agents (Hercules, Fabius, Janus).
- Never copy Claude prompts verbatim — rewrite for Devstral's principle-driven style.
- Never create a "catch-all" skill that tries to replicate all agents in one SKILL.md.
- Never write INSTALL.md before all target file paths in the repo are confirmed.
- Never run a shell script as part of install — the LLM drives the full setup via Vibe tools.
- Never add MCP server config to skill SKILL.md frontmatter (skills reference, not configure).

---

## Reference Links

- oh-my-vibe repository: `https://github.com/oniwakaa/oh-my-vibe`
- Mistral Vibe CLI repo: `https://github.com/mistralai/mistral-vibe`
- Mistral Vibe install: `curl -LsSf https://mistral.ai/vibe/install.sh | bash`
- Agent Skills specification: `https://agentskills.io/specification`
- Devstral model card: `https://huggingface.co/mistralai/Devstral-Small-2505`
