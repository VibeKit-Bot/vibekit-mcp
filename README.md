# vibekit-mcp

[![smithery badge](https://smithery.ai/badge/vibekit/vibekit-mcp)](https://smithery.ai/servers/vibekit/vibekit-mcp)

MCP server for VibeKit, deploy apps, manage hosting, and chat with AI agents from any MCP client.

This package is for **VibeKit cloud/API access**. It does **not** connect your local Claude Code instance to Telegram. For local-machine remote control, use `vibekit-agent`.

## Use it remotely (no install)

VibeKit also runs as a hosted remote server, so clients that accept a remote MCP URL (claude.ai web connectors, ChatGPT, etc.) need **no install**:

```
https://mcp.vibekit.bot/mcp?api_key=vk_your_api_key_here
```

Paste that URL into your client's "custom connector" / "remote MCP server" field. Clients that let you set headers can instead send `Authorization: Bearer vk_your_api_key_here` and use the bare `https://mcp.vibekit.bot/mcp`. See [Get an API key](#get-an-api-key) below.

Prefer a local stdio install (e.g. Claude Desktop)? Use the steps below.

## Get an API key

Keys start with `vk_`. Two ways to get one:

- **Instant, no signup:** one request returns a key.
  ```bash
  curl -X POST https://vibekit.bot/api/v1/auth/register
  # Response: {"apiKey": "vk_...", "plan": "free", "credits": 0}
  ```
  Save the returned key and reuse it. Each call to `/auth/register` creates a brand-new account, so call it once, not per request.
- **From your account:** if you already use VibeKit, copy or regenerate your key in the [web dashboard](https://app.vibekit.bot) or the iOS app settings.

## Installation

```bash
npm install -g vibekit-mcp
```

## Setup

1. Get a VibeKit API key (see [Get an API key](#get-an-api-key) above).

2. Add to your MCP client config (e.g. Claude Desktop) (`~/Library/Application Support/Claude/claude_desktop_config.json` on macOS):

```json
{
  "mcpServers": {
    "vibekit": {
      "command": "vibekit-mcp",
      "env": {
        "VIBEKIT_API_KEY": "vk_your_api_key_here"
      }
    }
  }
}
```

3. Restart your MCP client

## Available Tools

### Hosting

| Tool | Description |
|------|-------------|
| `vibekit_list_apps` | List all hosted apps |
| `vibekit_get_app` | Get details about a specific app |
| `vibekit_list_templates` | List starter templates for `vibekit_create_app` |
| `vibekit_create_app` | Create new app from a template |
| `vibekit_deploy` | Deploy GitHub repo to hosting |
| `vibekit_redeploy` | Redeploy app with latest code |
| `vibekit_list_deploys` | List an app's recent deploys with status and commit |
| `vibekit_rollback_deploy` | Roll an app back to a previous deploy |
| `vibekit_app_logs` | Get application logs |
| `vibekit_restart_app` | Restart an app |
| `vibekit_stop_app` | Stop an app |
| `vibekit_start_app` | Start a stopped app |
| `vibekit_app_env` | Get app environment variables |
| `vibekit_set_env` | Set app environment variables |
| `vibekit_delete_app` | Delete an app permanently |

### Agent

| Tool | Description |
|------|-------------|
| `vibekit_chat` | Chat with an app's AI agent |
| `vibekit_agent_status` | Get agent status |
| `vibekit_agent_history` | Get chat history with agent |

### Database

| Tool | Description |
|------|-------------|
| `vibekit_enable_database` | Enable a Postgres database for an app |
| `vibekit_database_status` | Get database status and connection info |
| `vibekit_db_schema` | Get the database schema (every table and its columns) |
| `vibekit_db_query` | Run a read-only SQL query (SELECT only, up to 200 rows) |
| `vibekit_db_table` | Browse one table's rows with pagination and sorting |

### QA

| Tool | Description |
|------|-------------|
| `vibekit_run_qa` | Run automated QA tests |
| `vibekit_qa_status` | Get QA test results |

### Tasks

| Tool | Description |
|------|-------------|
| `vibekit_submit_task` | Submit a coding task |
| `vibekit_get_task` | Get task status/result |
| `vibekit_list_tasks` | List recent tasks |
| `vibekit_wait_for_task` | Wait for task completion |
| `vibekit_cancel_task` | Cancel a running task |
| `vibekit_create_schedule` | Create recurring scheduled task |
| `vibekit_list_schedules` | List scheduled tasks |
| `vibekit_delete_schedule` | Delete scheduled task |

### Account

| Tool | Description |
|------|-------------|
| `vibekit_account` | Get account info (plan, credits, usage) |
| `vibekit_list_skills` | List implementation skills |
| `vibekit_get_skill` | Fetch specific skill content |

## Example Usage

Once configured, you can use prompts like:

- "Deploy my GitHub repo to VibeKit and create a new app"
- "Chat with the AI agent for my app about adding a contact form"
- "Show me the logs for my app and restart it if there are errors"
- "Enable a database for my app, then show me its schema and query the users table"
- "List my app's recent deploys and roll back to the last working one"
- "Run QA tests on my deployed app"
- "Check my VibeKit account balance and list my apps"
- "Create a weekly schedule to improve my app's performance"

## Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `VIBEKIT_API_KEY` | Your VibeKit API key (required) | none |
| `VIBEKIT_API_URL` | API base URL | `https://vibekit.bot/api/v1` |

## Related Packages

- `vibekit-cli`: terminal client for VibeKit cloud workflows
- `vibekit-agent`: Telegram bridge for local Claude Code on your own machine

## Links

- [VibeKit Website](https://vibekit.bot)
- [API Documentation](https://vibekit.bot/SKILL.md)
- [Dashboard](https://app.vibekit.bot) (view or regenerate your API key)
- [GitHub](https://github.com/VibeKit-Bot/vibekit-mcp)
