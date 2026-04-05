# Arquestra — MCP Plugin

Connects AI agents to [Arquestra](https://arquestra.ai) by Apertura AI — an AI orchestration platform for scientific computing, computational chemistry, and HPC workflows.

**MCP endpoint:** `https://api.arquestra.ai/mcp/orchestration`  
**Auth:** OAuth 2.0 PKCE (no token pasting) · Bearer machine token fallback

---

## Claude Code

### Option A — OAuth (recommended, no token pasting)

Install from Claude Code:
- Open **Manage Plugins** → search by GitHub URL
- Enter: `https://github.com/apertura-ai/arquestra-claude-plugin`
- Click **Install**

Claude Code opens `https://arquestra.ai/oauth/connect` in your browser — sign in with your Arquestra account. Done.

### Option B — machine token

```bash
claude mcp add arquestra \
  --transport http \
  --url https://api.arquestra.ai/mcp/orchestration \
  --header "Authorization: Bearer arqmt_..."
```

Get your token at [arquestra.ai](https://arquestra.ai) → workspace setup → Local Runtime.

---

## OpenAI Codex CLI

Add to `~/.codex/config.toml`:

```toml
[mcp_servers.arquestra]
url = "https://api.arquestra.ai/mcp/orchestration"
# Bearer machine token fallback (OAuth not yet supported by Codex)
bearer_token_env_var = "ARQUESTRA_MACHINE_TOKEN"
```

Set the env var:
```bash
# macOS / Linux
echo 'export ARQUESTRA_MACHINE_TOKEN="arqmt_..."' >> ~/.zshrc

# Windows PowerShell
[System.Environment]::SetEnvironmentVariable("ARQUESTRA_MACHINE_TOKEN","arqmt_...","User")
```

---

## GitHub Copilot / VS Code

Requires VS Code 1.101+. Add to `.vscode/mcp.json` (workspace) or user MCP settings:

### Option A — OAuth auto-discovery (VS Code 1.101+)

```json
{
  "servers": {
    "arquestra": {
      "type": "http",
      "url": "https://api.arquestra.ai/mcp/orchestration"
    }
  }
}
```

VS Code discovers the OAuth server automatically via `/.well-known/oauth-authorization-server` and opens the browser sign-in flow.

### Option B — machine token

```json
{
  "servers": {
    "arquestra": {
      "type": "http",
      "url": "https://api.arquestra.ai/mcp/orchestration",
      "headers": {
        "Authorization": "Bearer ${input:arquestra_token}"
      }
    }
  },
  "inputs": [
    {
      "type": "promptString",
      "id": "arquestra_token",
      "description": "Arquestra machine token (arqmt_…)",
      "password": true
    }
  ]
}
```

---

## Available tools

| Tool | Description |
|---|---|
| `create_run` | Start a new run — returns `run_id`, token, and MCP URL to enter the full orchestration loop |
| `list_runs` | List your runs, newest first |
| `get_run` | Get status and details for a specific run |
| `get_run_logs` | Fetch current state and logs for a run |
| `list_machines` | List your registered runner machines |
| `list_packs` | List available domain packs (chemistry, HPC, bioinformatics…) |

---

## Auth

**OAuth 2.0 PKCE** (recommended): supported by Claude Code and Copilot/VS Code. The API server exposes `/.well-known/oauth-authorization-server` — agents that support OAuth auto-discovery will handle the login flow automatically.

**Machine token** (`arqmt_…`) fallback: for agents that don't support OAuth yet (Codex CLI) or for headless environments. Generate one at [arquestra.ai](https://arquestra.ai) → workspace setup.

---

## Links

- [Arquestra](https://arquestra.ai)
- [Apertura AI](https://apertura.ai)
- [MCP endpoint docs](https://api.arquestra.ai/mcp/orchestration)
- [OAuth server metadata](https://api.arquestra.ai/.well-known/oauth-authorization-server)
