---
name: dzine-authentication
description: Connect Dzine Pipeline Local during plugin setup, or recover when its MCP connection has a missing, expired, revoked, or rejected token or a tool reports an explicit authentication failure.
---

# Dzine Pipeline Local authentication

## Connect or recover

Use the host's connection/authentication action for this plugin when credentials are missing, HTTP 401 is returned, or a Dzine tool explicitly reports an invalid, expired, revoked, or rejected token. Suspend dependent Dzine calls until authorization completes.

1. If an existing authorization has expired, been revoked, or been rejected, use Codex's disconnect or sign-out action for Dzine Pipeline Local to clear all locally stored OAuth credentials for that connection. Keep the browser's Dzine sign-in session and other connections intact. If Codex requires the user to take this action, guide them to the connection settings. A first-time connection can proceed directly to authorization.
2. Open the Dzine Pipeline Local connection in Codex and start a fresh authorization.
3. Let the host open the authorization URL and follow the service's redirect to the Dzine consent page. Ask the user to sign into Dzine and select Allow.
4. Let the authorization service complete the host-provided callback and token exchange. Keep tokens out of chat messages, prompts, plugin files, and custom deep-link query parameters.
5. After the host confirms connection, verify access with `list_projects`. Resume the user's original task when this succeeds.

Treat HTTP 403 or project/canvas membership denial as a resource permission failure unless the service explicitly identifies invalid credentials. Explain which access is missing.

After reconnecting, retry failed reads once. For writes, asset creation, or generation with an uncertain submission outcome, reconcile using the original operation ID and `get_operation` before resubmitting. Preserve the original operation ID. If reconciliation is unavailable, report the uncertain outcome and stop automatic resubmission.

If Codex cannot reach Dzine Pipeline Local, tell the user the local connection is unavailable and ask them to contact their Dzine support contact. If the user cancels or authorization fails again, explain what happened and stop retrying.
