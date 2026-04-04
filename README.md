# Arquestra — Claude Code Plugin

Connects Claude Code to [Arquestra](https://arquestra.ai) by Apertura AI — an AI orchestration platform for scientific computing, computational chemistry, and HPC workflows.

## Setup

1. Install this plugin in Claude Code:
   - Open Manage Plugins → search by GitHub URL
   - Enter: `https://github.com/apertura-ai/arquestra-claude-plugin`
   - Click Install

2. Claude Code will open `https://arquestra.ai/oauth/connect` in your browser — sign in with your Arquestra account to authorize.

That's it. No token pasting required.

## Available tools

| Tool | Description |
|---|---|
| `create_run` | Start a new Arquestra run — returns `run_id`, token, and MCP URL to enter the orchestration loop |
| `list_runs` | List your runs, ordered newest first |
| `get_run` | Get status and details for a specific run |
| `get_run_logs` | Fetch current state and summary for a run |
| `list_machines` | List your registered runner machines |
| `list_packs` | List available domain packs (chemistry, HPC, bioinformatics…) |

## Auth

Authentication uses **OAuth 2.0 Authorization Code + PKCE** — the same pattern used by Supabase, Vercel, and Neon plugins. The flow:

1. Claude Code opens the Arquestra authorization URL in your browser
2. You sign in with your existing Arquestra/Clerk account
3. Claude Code receives an access token — stored locally, refreshed automatically
4. All requests to `/mcp/orchestration` are scoped to your account

**Fallback:** If you prefer a static token, you can still use a machine token (`arqmt_…`) from your workspace settings:
```bash
claude mcp add arquestra-fallback \
  --transport http \
  --url https://api.arquestra.ai/mcp/orchestration \
  --header "Authorization: Bearer arqmt_..."
```

## Links

- [Arquestra](https://arquestra.ai)
- [Apertura AI](https://apertura.ai)
- [Documentation](https://arquestra.ai/docs)
