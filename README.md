# Arquestra — Claude Code Plugin

Connects [Claude Code](https://claude.ai/code) to [Arquestra](https://apertura-ai.de) by Apertura AI — an AI orchestration platform for scientific computing, computational chemistry, and HPC workflows.

**MCP endpoint:** `https://api.apertura-ai.de/mcp/orchestration`  
**Auth:** OAuth 2.0 PKCE (no token pasting)

---

## Install

### Via Claude Code Plugin Manager (recommended)

1. Open **Manage Plugins** → Install by GitHub URL
2. Enter: `https://github.com/Apertura-AI/arquestra-claude-plugin`
3. Click **Install**

Claude Code opens `https://apertura-ai.de/oauth/connect` in your browser — sign in with your Arquestra account. Done. The token is stored locally for 90 days and refreshed automatically.

### Via Arquestra Runner (automatic)

If you have the [Arquestra Runner](https://apertura-ai.de) installed, the plugin is configured automatically:

```bash
arquestra-runner configure-mcp --agent claude
```

This registers the plugin and handles OAuth on first connection.

---

## Available tools

| Tool | Description |
|---|---|
| `cloud_mcp_probe` | Verify cloud MCP connection |
| `create_run` | Start a new run — returns `run_id` and enters the orchestration loop |
| `list_runs` | List your runs, newest first |
| `get_run` | Get status and details for a specific run |
| `get_run_logs` | Fetch current state and logs for a run |
| `list_machines` | List your registered runner machines |
| `list_packs` | List available domain packs (chemistry, HPC, bioinformatics…) |

---

## Auth

**OAuth 2.0 PKCE** — the API exposes `/.well-known/oauth-authorization-server`. Claude Code handles the login flow automatically on first connection. No tokens to paste or manage.

---

## Other agents

For Codex CLI, Gemini CLI, VS Code, Cursor, and others — use the Arquestra Runner:

```bash
arquestra-runner configure-mcp --agent all
```

This writes the correct MCP config for each detected agent automatically.

---

## Links

- [Arquestra](https://apertura-ai.de)
- [Apertura AI](https://github.com/Apertura-AI)
- [OAuth server metadata](https://api.apertura-ai.de/.well-known/oauth-authorization-server)
