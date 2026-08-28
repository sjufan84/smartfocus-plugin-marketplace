# SmartFocus Claude Code Plugin

Run SmartFocus AI focus groups from Claude Code and get qualitative feedback on designs, features, and concepts without leaving the development workflow.

## Setup

1. Install this plugin directory with Claude Code's plugin installer.
2. Authenticate the SmartFocus MCP server when Claude Code prompts you.
3. Sign in through SmartFocus and approve the requested access.

The hosted gateway uses WorkOS OAuth. No SmartFocus API key needs to be copied into the plugin environment.

## Usage

Ask Claude Code to run a focus group, or use `/run-focus-group`.

Examples:

- "Run a focus group testing this landing page with small business owners."
- "Get feedback on this checkout flow from mobile-first shoppers aged 25-40."
- "Follow up with the same panel about the updated design."

## Tools

| Tool | Description |
| --- | --- |
| `run_focus_group` | Create and run a focus group end to end |
| `get_status` | Poll for progress |
| `get_results` | Retrieve the report, transcript, and recommendations |
| `follow_up` | Continue with the same participant panel |
| `generate_focus_group_plan` | Not yet implemented - returns a notice |

## Requirements

- SmartFocus account with MCP access
- Browser access for the initial WorkOS authorization

The initial release uses an Azure Container Apps managed HTTPS hostname. A future plugin version can switch to `mcp.smartfocus.ai` after SmartFocus DNS is available.
