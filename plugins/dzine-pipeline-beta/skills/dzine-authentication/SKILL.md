---
name: dzine-authentication
description: Connect Dzine Pipeline during plugin setup, or recover when its MCP connection has a missing, expired, revoked, or rejected token or a tool reports an explicit authentication failure.
---

# Dzine Pipeline authentication

Use the host's connection/authentication action for this plugin when credentials are missing, HTTP 401 is returned, or a Dzine tool explicitly reports an invalid, expired, revoked, or rejected token. Suspend dependent Dzine calls until authorization completes.

1. Start the host-provided MCP authorization flow for Dzine Pipeline. For a separately configured CLI MCP entry, use `codex mcp login <registered-server-name>` with its actual registered name.
2. Let the host open the authorization URL. The Codex consent page is [Dzine MCP authentication](http://beta.stylardesign.com/mcp-authentication?type=codex). Preserve the authorization request parameters provided by the service. Ask the user to sign into Dzine and select Allow.
3. Let the authorization service complete the host-provided callback and token exchange. Keep tokens out of chat messages, prompts, plugin files, and custom deep-link query parameters.
4. After the host confirms connection, verify access with `list_projects`. Resume the user's original task when this succeeds.

Treat HTTP 403 or project/canvas membership denial as a resource permission failure unless the service explicitly identifies invalid credentials. Explain which access is missing.

After reconnecting, retry failed reads once. For writes, asset creation, or generation with an uncertain submission outcome, reconcile using the original operation ID and `get_operation` before resubmitting. Preserve the original operation ID. If reconciliation is unavailable, report the uncertain outcome and stop automatic resubmission.

If authorization is cancelled, fails again, or the service lacks OAuth discovery/token exchange, report the blocker and stop the recovery loop. Opening the consent page alone does not establish an authenticated connection.

## Current implementation boundary

The plugin currently uses `DZINE_MCP_TOKEN` via `bearer_token_env_var`. The React consent page is implemented, but its Allow action and the MCP OAuth endpoints are pending. Until they are connected, explain that browser authorization is unavailable and the current manual setup requires launching Codex with a valid `DZINE_MCP_TOKEN` in its environment. These instructions define the recovery workflow; the MCP service must implement the authentication challenge and OAuth endpoints for the host to initiate it automatically.
