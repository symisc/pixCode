# pixCode Documentation

> The AI coding agent that lives in your terminal.
> Powered by the [PixLab](https://pixlab.io) LLM SSE backend.
> Long context, tools, and programmable workflows —<br>
  start in the terminal, scale to desktop and beyond.

---


## Getting Started

| Page | What you'll learn |
|---|---|
| **[Getting Started Guide](start.md)** | Step-by-step walkthrough: install, onboarding, first prompt, VS Code extension |
| **[Quickstart](quickstart.md)** | Install pixCode and start coding in 60 seconds |
| **[Download & Install](download.md)** | All installation methods (curl, Homebrew, npm, VS Code extension, manual) |
| **[Features](features.md)** | Everything pixCode can do — multi-provider, streaming, tools, slash commands, MCP, workflows |
| **[FAQ](faq.md)** | Frequently asked questions |

---

## Configuration

| Page | What you'll learn |
|---|---|
| **[Configuration](configuration.md)** | Config files, settings, model selection, permissions, retry, shell |
| **[Providers](providers.md)** | PixLab provider setup, available models, API key configuration |
| **[Slash Commands](slash-commands.md)** | Complete reference for all `/` commands |
| **[Privacy](privacy.md)** | What data pixCode collects and how it's protected |
| **[Pricing](pricing.md)** | PixLab pricing and cost estimation |

---

## Extensions & Customization

| Page | What you'll learn |
|---|---|
| **[Skills](skills.md)** | Reusable instruction folders that teach pixCode a workflow or domain pattern |
| **[Plugins](plugins.md)** | Install slash commands, skills, subagents, rules, MCP servers, and hooks |
| **[Hooks](hooks.md)** | Run shell scripts at lifecycle points (session start, tool call, turn end) |
| **[MCP Servers](mcp.md)** | Connect pixCode to any Model Context Protocol server for external tools |
| **[Subagents](agents.md)** | Define focused child-agent roles such as reviewers or researchers |
| **[Workflows](workflows.md)** | Write JavaScript scripts that orchestrate multi-agent pipelines |
| **[Custom Workflows](custom-workflows.md)** | Advanced workflow authoring guide |

---

## Quick Reference

### Install

```bash
# macOS / Linux
curl -fsSL https://raw.githubusercontent.com/symisc/pixcode/main/scripts/install.sh | sh

# Windows (PowerShell)
irm https://raw.githubusercontent.com/symisc/pixcode/main/scripts/install.ps1 | iex

# Homebrew
brew install pixlab/tap/pixcode

# npm (all platforms)
npm install -g pixcode
```

### Set Your API Key

```bash
pixcode setup
```

Or set the environment variable:

```bash
export PIXLAB_API_KEY=your-key-here
```

Get a key at **[console.pixlab.io](https://console.pixlab.io/)**.

### Launch

```bash
# Interactive TUI
pixcode

# One-shot prompt
pixcode exec "explain this codebase"

# Resume a session
pixcode resume --last
```

### Key Slash Commands

| Command | What it does |
|---|---|
| `/help` | Show all available commands |
| `/setup` | Interactive onboarding wizard |
| `/auth` | Set or update your API key |
| `/provider` | Switch LLM provider |
| `/model` | Choose model, effort, and thinking |
| `/compact` | Compress conversation context |
| `/review` | Review changes, a branch, a PR, or a commit |
| `/resume` | Open session resume picker |
| `/permissions` | Configure auto-accept or auto-review |
| `/doctor` | Diagnose your setup |
| `/exit` or `/quit` | Exit pixCode |

---

## CLI Flags

```
pixcode [flags]
pixcode [command]
```

| Flag | Description |
|---|---|
| `--about` | Show about information and exit |
| `--list-models` | List available models and exit |
| `--list-providers` | List supported LLM providers and exit |
| `--list-sessions` | List recent sessions and exit |
| `--resume` | Resume a session (picker, or pass a session id) |
| `-m, --model` | Model to use (flash\|pro\|max) |
| `--effort` | Override reasoning effort (high\|max) |
| `--thinking` | Override thinking for this run |
| `--data-dir` | Override the data directory (default: ~/.pixcode) |
| `--config` | Path to a custom config file |
| `--no-color` | Disable ANSI colors |
| `-q, --quiet` | Minimal output |
| `-v, --verbose` | Verbose output with debug logs |
| `--print-session-id` | Print session ID on exit |
| `--no-update-check` | Skip update check |
| `-V, --version` | Print version and exit |
| `-w, --worktree` | Create or reuse an isolated git worktree |

### Subcommands

| Command | Description |
|---|---|
| `pixcode exec [prompt]` | Run a single prompt non-interactively |
| `pixcode resume [id]` | Resume a session (picker, `--last`, or pass an id) |
| `pixcode setup` | Save your PixLab API key |
| `pixcode doctor` | Run health checks |
| `pixcode plugin` | Manage plugins |

---

## Environment Variables

| Variable | Description |
|---|---|
| `PIXLAB_API_KEY` | PixLab API key (overrides credentials file) |
| `PIXLAB_BASE_URL` | Override the PixLab endpoint URL |
| `PIXCODE_HOME` | Override the data directory (default: ~/.pixcode) |
| `PIXCODE_LANG` | Override the detected locale (en, fr, es, de, zh, ja) |

---

## Architecture

pixCode is a single Go binary with zero runtime dependencies.

```
cmd/pixcode/          Entry point
internal/
  ui/cli/             Cobra CLI commands and flags
  tui/                Bubbletea terminal UI
  agent/              Turn loop, approvals, hooks, tool orchestration
  tools/              Built-in tools (shell, patch, file, web)
  app/                Runtime state, config, credentials, providers
  llm/pixlab/         PixLab SSE streaming client
  secrets/            AES-256-GCM credential encryption
  l10n/               Localization (6 locales)
  session/            Session management
  store/              JSONL persistence
  mcp/                Model Context Protocol support
  skills/             Skill loading and management
  plugins/            Plugin system
  workflow/           JavaScript workflow engine
  worktree/           Git worktree isolation
  evals/              Evaluation harness
```

---

## Links

- **[GitHub Repository](https://github.com/symisc/pixcode)**
- **[Issue Tracker](https://github.com/symisc/pixcode/issues)**
- **[Releases](https://github.com/symisc/pixcode/releases)**
- **[Contributing](../CONTRIBUTING.md)**
- **[Security Policy](../SECURITY.md)**
- **[Roadmap](../ROADMAP.md)**
- **[Code of Conduct](../CODE_OF_CONDUCT.md)**

---

*pixCode is open source and licensed under the MIT License.*
