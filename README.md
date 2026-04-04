# Arquestra — Claude Code Plugin

Connects Claude Code to [Arquestra](https://arquestra.ai) by Apertura AI — an AI orchestration platform for scientific computing, computational chemistry, and HPC workflows.

## Setup

1. Get your machine token from [arquestra.ai](https://arquestra.ai) (workspace setup → Local Runtime)

2. Set the environment variable:
   ```bash
   # macOS / Linux
   echo 'export ARQUESTRA_MACHINE_TOKEN="arqmt_..."' >> ~/.zshrc

   # Windows PowerShell
   [System.Environment]::SetEnvironmentVariable("ARQUESTRA_MACHINE_TOKEN","arqmt_...","User")
   ```

3. Install this plugin in Claude Code:
   - Open Manage Plugins → search by GitHub URL
   - Enter: `https://github.com/apertura-ai/arquestra-claude-plugin`
   - Click Install

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

Authentication uses your personal **machine token** (`arqmt_…`), the same token used by the local runner. It is scoped to your account — only your runs, machines, and packs are accessible. The token is never stored in this plugin; it is read from `ARQUESTRA_MACHINE_TOKEN` at runtime.

The Arquestra API enforces Clerk-based access control. Tokens are validated server-side on every request.

## Links

- [Arquestra](https://arquestra.ai)
- [Apertura AI](https://apertura.ai)
- [Documentation](https://arquestra.ai/docs)
