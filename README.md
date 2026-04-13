# oh-my-vibe

A community port of [oh-my-openagent](https://github.com/code-yeongyu/oh-my-openagent)
for [Mistral Vibe CLI](https://github.com/mistralai/mistral-vibe).

oh-my-vibe brings the full oh-my-openagent multi-agent ecosystem — 11 specialized
agents and 10 slash-command skills — to the Mistral Vibe CLI, optimized for
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

| Command | Description |
|---|---|
| `/ultrawork` | Full-auto mode: intent gate → plan → delegate → verify |
| `/ulw` | Alias for `/ultrawork` |
| `/ulw-loop` | Continuous ultrawork loop until todo is empty |
| `/interview-me` | Janus interview mode: questions → plan |
| `/plan` | Direct planning mode (no interview) |
| `/start-work` | Hand latest Janus plan to Fabius |
| `/censor` | Gap analysis — find what the plan is missing |
| `/cato` | Plan review — APPROVED / NOT APPROVED verdict |
| `/init-deep` | Generate AGENTS.md hierarchy for the current project |
| `/ralph-loop` | Retry loop for the current task until 100% done |

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
https://raw.githubusercontent.com/code-yeongyu/oh-my-vibe/main/INSTALL.md
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

## File Layout

```
oh-my-vibe/
├── AGENTS.md                    ← workspace context (read by agents)
├── INSTALL.md                   ← one-line install prompt
├── README.md                    ← this file
├── config/
│   └── config.template.toml    ← global config template
├── agents/                      ← 11 agent TOML files
├── prompts/                     ← 11 Devstral-optimized system prompts
└── skills/                      ← 7 SKILL.md files with slash commands
```

---

## MCP Servers

oh-my-vibe configures three remote MCP servers in `config.template.toml`:

| Server | Purpose | Key Required |
|---|---|---|
| `websearch` | Web search via Exa | `EXA_API_KEY` |
| `context7` | Library documentation lookup | None |
| `grep_app` | OSS public code search | None |

MCP config must live in `~/.vibe/config.toml` (global). It cannot be placed in
individual agent TOML files.

---

## Design Notes

- **Devstral-optimized prompts.** All 11 prompts are written for Devstral's
  principle-driven, XML-tagged style — not copied verbatim from the Claude-specific
  source prompts.
- **Faithful port.** All 11 agents and all 10 skills from oh-my-openagent are
  preserved. No agent was collapsed or omitted.
- **LLM-driven install.** No shell scripts. The install is driven by pasting a prompt
  into Vibe CLI — the agent copies all files to the right locations.

---

## Source

Ported from [oh-my-openagent](https://github.com/code-yeongyu/oh-my-openagent) (branch: dev)
by the oh-my-vibe community. Original work by [@code-yeongyu](https://github.com/code-yeongyu).

## License

MIT
