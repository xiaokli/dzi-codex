---
name: dzine-authentication
description: Connect Dzine Pipeline Local during plugin setup, or recover when its MCP connection has a missing, expired, revoked, or rejected token or a tool reports an explicit authentication failure.
---

# Dzine Pipeline Local authentication

When credentials are missing, HTTP 401 is returned, or a Dzine tool explicitly reports an invalid, expired, revoked, or rejected token, use the manual setup below until the service supports OAuth. Suspend dependent Dzine calls until access is verified.

## Post-install setup

During plugin onboarding, guide the user through these steps before calling Dzine tools. Use the same steps to replace an expired or rejected token.

1. Open the user-level Codex config at `~/.codex/config.toml`. Add the following settings, updating existing tables in place if present. The first table disables the connection bundled with the plugin. The second registers a personal connection with a configurable Authorization header.

   ```toml
   [plugins."dzine-pipeline-local@dzine-codex-market".mcp_servers.dzine-pipeline-local]
   enabled = false

   [mcp_servers.dzine-pipeline-local]
   url = "http://127.0.0.1:4310/mcp"
   http_headers = { Authorization = "Bearer <DZINE_MCP_TOKEN>" }
   ```

2. Replace `<DZINE_MCP_TOKEN>` directly in the local config with a valid Dzine token and keep the `Bearer ` prefix. Keep the real token out of chat, source control, and distributed plugin packages.
3. Restart Codex and confirm `dzine-pipeline-local` appears under **Servers** in MCP settings. Verify access with `list_projects`.

## OAuth recovery

Use this flow once the service supports OAuth.

1. Start the host-provided MCP authorization flow for Dzine Pipeline Local. For a separately configured CLI MCP entry, use `codex mcp login dzine-pipeline-local`.
2. Let the host open the authorization URL. The Codex consent page is [Dzine MCP authentication](http://localhost:5171/mcp-authentication?type=codex). Preserve the authorization request parameters provided by the service. Ask the user to sign into Dzine and select Allow.
3. Let the authorization service complete the host-provided callback and token exchange. Keep tokens out of chat messages, prompts, plugin files, and custom deep-link query parameters.
4. After the host confirms connection, verify access with `list_projects`. Resume the user's original task when this succeeds.

Treat HTTP 403 or project/canvas membership denial as a resource permission failure unless the service explicitly identifies invalid credentials. Explain which access is missing.

After reconnecting, retry failed reads once. For writes, asset creation, or generation with an uncertain submission outcome, reconcile using the original operation ID and `get_operation` before resubmitting. Preserve the original operation ID. If reconciliation is unavailable, report the uncertain outcome and stop automatic resubmission.

If authorization is cancelled, fails again, or the service lacks OAuth discovery/token exchange, report the blocker and stop the recovery loop. Opening the consent page alone does not establish an authenticated connection.

## Current implementation boundary

The React consent page is implemented. Browser authorization requires the Allow action and the MCP OAuth endpoints to be connected.
