# oh-my-vibe

An agent and skill ecosystem for [Mistral Vibe CLI](https://github.com/mistralai/mistral-vibe).

oh-my-vibe brings a full multi-agent ecosystem — 11 specialized
agents and 26 slash-command skills — to the Mistral Vibe CLI, optimized for
[Devstral](https://huggingface.co/mistralai/Devstral-Small-2505).

---

## Agents

| Agent | Type | Role |
|---|---|---|
| **Hercules** | primary | Main orchestrator. Plans, delegates, verifies. Use for any complex task. |
| **Vulcan** | primary | Deep autonomous worker. Give a goal; it figures out how. |
| **Janus** | primary | Strategic planner. Interviews you, produces a decision-complete plan. |
| **Fabius** | primary | Executes Janus plans via subagent delegation and todo tracking. |
| **Minerva** | primary | Read-only architect. Answers "how does this work" and "what should we do". |
| **Achates** | subagent | Scoped implementation worker delegated from Hercules or Fabius. |
| **Agrippa** | subagent | Fast codebase grep and pattern discovery. |
| **Varro** | subagent | Docs and OSS code search via websearch, context7, grep_app. |
| **Censor** | subagent | Gap analyzer. Reviews plans for missing decisions. |
| **Cato** | subagent | Ruthless plan reviewer. APPROVED / NOT APPROVED verdicts. |
| **Argus** | subagent | Vision agent. Reads screenshots, diagrams, UI states. |

## Slash Commands (Skills)

### Orchestration & Planning

| Command | Description |
|---|---|
| `/ultrawork` | Full-auto mode: intent gate → plan → delegate → verify |
| `/ulw` | Alias for `/ultrawork` |
| `/ulw-loop` | Continuous ultrawork loop until todo is empty |
| `/ultraworker` | Main orchestrator agent for complex multi-step tasks |
| `/interview-me` | Janus interview mode: questions → plan |
| `/plan` | Direct planning mode (no interview) |
| `/start-work` | Hand latest Janus plan to Fabius |
| `/ralph-loop` | Retry loop for the current task until 100% done |

### Plan Review

| Command | Description |
|---|---|
| `/censor` | Gap analysis — find what the plan is missing |
| `/cato` | Plan review — APPROVED / NOT APPROVED verdict |

### Quality & Verification

| Command | Description |
|---|---|
| `/review-work` | Post-implementation review: launches parallel verification swarm |
| `/ai-slop-remover` | Removes AI-generated code smells from a single file |
| `/remove-ai-slops` | Branch-wide AI slop removal and critical review |
| `/tdd-gate` | Enforces RED → GREEN → REFACTOR workflow for logic-heavy changes |
| `/handoff` | Creates a structured context summary for continuing work in a new session |

### Agent Switching

| Command | Description |
|---|---|
| `/hercules` | Switch to Hercules (main orchestrator) |
| `/vulcan` | Switch to Vulcan (deep autonomous worker) |
| `/janus` | Switch to Janus (strategic planner) |
| `/fabius` | Switch to Fabius (plan executor) |
| `/minerva` | Switch to Minerva (architecture consultant) |

### Browser & UI

| Command | Description |
|---|---|
| `/playwright` | Browser automation via Playwright MCP (testing, screenshots, scraping) |
| `/dev-browser` | Browser automation with persistent page state |
| `/frontend-ui-ux` | Designer-turned-developer for stunning UI/UX |

### Git & Project

| Command | Description |
|---|---|
| `/git-master` | Atomic commits, rebase/squash, history search (blame, bisect, log -S) |
| `/init-deep` | Generate AGENTS.md hierarchy for the current project |
| `/omv` | Display the oh-my-vibe boot message |

---

## Quickstart

### 1. Install Vibe CLI

```bash
curl -LsSf https://mistral.ai/vibe/install.sh | bash
```

### 2. Install oh-my-vibe

Paste this into any Vibe CLI session from inside the oh-my-vibe directory:

```
Install and configure oh-my-vibe by following the instructions here:
https://raw.githubusercontent.com/oniwakaa/oh-my-vibe/main/INSTALL.md
```

The agent will read the install instructions and set everything up automatically.
See [INSTALL.md](./INSTALL.md) for details.

### 3. Configure

Copy `config/config.template.toml` to `~/.vibe/config.toml` (or merge it with your
existing config) and set your API key:

```bash
# API key
export MISTRAL_API_KEY="your_key_here"

# If using websearch (optional)
export EXA_API_KEY="your_exa_key"
```

### 4. Use an agent

```bash
# Main orchestrator (recommended starting point)
vibe --agent hercules

# Strategic planner
vibe --agent janus

# Deep autonomous worker
vibe --agent vulcan
```

### 5. Use slash commands

Inside any Vibe session:

```
/ultrawork Implement rate limiting on the /api/v1/users endpoint
/interview-me I want to add MongoDB support to the data layer
/plan Add pagination to search results
/start-work
```

---

## Uninstalling

To remove oh-my-vibe entirely, leaving your pre-existing Vibe CLI configuration unmodified, paste this into any Vibe session:

```
Uninstall oh-my-vibe by following the instructions here:
https://raw.githubusercontent.com/oniwakaa/oh-my-vibe/main/UNINSTALL.md
```

See [UNINSTALL.md](./UNINSTALL.md) for details.

---

## Agent Tools

Each agent has a specific set of Vibe CLI tools available. The orchestrator agents
(Hercules, Vulcan, Fabius) have the full toolkit including LSP, AST-grep, and
session management. Read-only agents (Minerva, Censor, Cato) have restricted tool access.

Key tools available to appropriate agents:

| Tool | Purpose | Available To |
|---|---|---|
| `lsp_diagnostics` | Type-check and lint files | Hercules, Vulcan, Fabius, Achates, Janus, Minerva |
| `lsp_goto_definition` | Jump to symbol definition | Hercules, Vulcan, Fabius, Achates, Janus, Minerva |
| `lsp_find_references` | Find all symbol usages | Hercules, Vulcan, Fabius, Achates, Janus, Minerva |
| `lsp_rename` | Rename symbol across workspace | Hercules, Vulcan, Fabius, Achates |
| `lsp_symbols` | List symbols in file/workspace | All agents with `lsp_*` tools |
| `ast_grep_search` | AST-aware pattern search | Hercules, Vulcan, Fabius, Achates, Janus, Minerva, Censor, Cato, Agrippa |
| `ast_grep_replace` | AST-aware pattern rewrite | Hercules, Vulcan, Fabius, Achates |
| `glob` | File pattern matching | Hercules, Vulcan, Fabius, Achates, Janus, Minerva, Censor, Cato, Agrippa |
| `look_at` | Image/screenshot analysis | Hercules, Argus |
| `session_list` | List conversation sessions | Hercules, Vulcan, Janus, Minerva |
| `session_read` | Read session history | Hercules, Vulcan, Janus, Minerva, Fabius |
| `session_search` | Search session history | Hercules, Vulcan, Janus, Minerva, Fabius |

---

## MCP Servers

oh-my-vibe configures three remote MCP servers in `config.template.toml`:

| Server | Purpose | Key Required |
|---|---|---|
| `websearch` | Web search via Exa | `EXA_API_KEY` |
| `context7` | Library documentation lookup | None |
| `grep_app` | OSS public code search | None |

An optional Playwright MCP server is included (commented out) for browser automation:

| Server | Purpose | Key Required |
|---|---|---|
| `playwright` | Browser automation, testing, screenshots | None (requires Node.js) |

MCP config must live in `~/.vibe/config.toml` (global). It cannot be placed in
individual agent TOML files.

---

## File Layout

```
oh-my-vibe/
├── AGENTS.md                    ← workspace context (read by agents)
├── INSTALL.md                   ← one-line install prompt
├── README.md                    ← this file
├── UNINSTALL.md                 ← uninstall instructions
├── config/
│   └── config.template.toml    ← global config template with MCP servers
├── agents/                      ← 11 agent TOML files
├── prompts/                     ← 11 Devstral-optimized system prompts
└── skills/                      ← 26 SKILL.md files with slash commands
    ├── ultrawork/
    ├── ulw/
    ├── ulw-loop/
    ├── ultraworker/
    ├── interview-me/
    ├── plan/
    ├── start-work/
    ├── ralph-loop/
    ├── censor/
    ├── cato/
    ├── review-work/
    ├── ai-slop-remover/
    ├── remove-ai-slops/
    ├── tdd-gate/
    ├── handoff/
    ├── init-deep/
    ├── omv/
    ├── hercules/
    ├── vulcan/
    ├── fabius/
    ├── janus/
    ├── minerva/
    ├── playwright/
    ├── git-master/
    ├── frontend-ui-ux/
    └── dev-browser/
```

---

## Design Notes

- **Devstral-optimized prompts.** All 11 prompts are written for Devstral's
  principle-driven, XML-tagged style — not copied verbatim from the Claude-specific
  source prompts. Each prompt includes behavioral instructions ported from the
  open-source Sisyphus orchestrator: intent gating, anti-duplication rules, failure
  recovery protocols, session continuity, evidence requirements, and tone/style guidance.
- **Complete Toolkit.** All 11 agents have Vibe CLI tool access matching their roles,
  including LSP diagnostics, AST-grep, session management, and glob where appropriate.
- **Complete Skill Set.** All 26 skills are included natively, covering orchestration,
  planning, review, quality gates, agent switching, browser automation, git operations,
  UI/UX design, and project initialization.
- **LLM-driven install.** No shell scripts. The install is driven by pasting a prompt
  into Vibe CLI — the agent copies all files to the right locations.

---

## License

MIT