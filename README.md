# Arquestra — Claude Code Plugin

Connects [Claude Code](https://claude.ai/code) to [Arquestra](https://apertura-ai.de) by Apertura AI — an AI orchestration platform for scientific computing, computational chemistry, and HPC workflows.

**MCP endpoint:** `https://api.apertura-ai.de/mcp/orchestration`  
**Auth:** OAuth 2.0 PKCE — sign in once with your Arquestra account, token stored for 90 days.

---

## Install

### Via Arquestra Runner (recommended — automatic)

If you have the [Arquestra Runner](https://apertura-ai.de) installed:

```bash
arquestra-runner configure-mcp --agent all
```

This registers the plugin automatically. On first use, Claude Code opens `https://apertura-ai.de/oauth/connect` in your browser. If you are already signed into your Arquestra account there, authorization completes instantly with no extra steps. If not, sign in once and you are done.

### Via Claude Code Plugin Manager (manual fallback)

1. Open **Manage Plugins** → Install by GitHub URL
2. Enter: `https://github.com/Apertura-AI/arquestra-claude-plugin`
3. Click **Install**
4. On first use, Claude Code opens `https://apertura-ai.de/oauth/connect` — sign in if not already authenticated.

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

**OAuth 2.0 PKCE** — the API exposes `/.well-known/oauth-authorization-server`. Claude Code handles the full login flow on first connection. No tokens to paste or manage. The 90-day access token is stored locally and renewed on expiry.

---

## Other agents

For Codex CLI, Gemini CLI, VS Code, Cursor, and others — the runner covers them too:

```bash
arquestra-runner configure-mcp --agent all
```

---

## Links

- [Arquestra](https://apertura-ai.de)
- [Apertura AI](https://github.com/Apertura-AI)
- [OAuth server metadata](https://api.apertura-ai.de/.well-known/oauth-authorization-server)
