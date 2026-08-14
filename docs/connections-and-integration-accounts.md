---
title: Connections and integration accounts
description: Add, edit, test, and delete integration accounts in Clay's Connections settings, and set default accounts for your workspace.
last_synced: 2026-04-26T01:40:56.525Z
---

# Connections and integration accounts

Use this article to add integration accounts in Clay's `Connections` settings, edit or test their credentials, set default accounts, and delete accounts you no longer need.

Clay consolidates multiple data providers into a single platform and integrates with your tech stack through 100+ available integrations. The `Connections` settings allow you to manage these integrations with external services. Each integration is represented as an `account` with its own authentication and configuration.

You can connect multiple accounts to the same integration for added flexibility, designate default accounts for specific integrations, and modify, reconnect, or remove accounts as needed. For admin controls over who can add and use connections, see [Access settings for connections](./access-settings-for-connections.md).

## What is an integration account?

An **integration account** is a configured connection between your workspace and an external service, such as an API or data provider. Each account enables your workspace to authenticate and interact with the service to perform specific tasks or access features.

-   `Account / Key Name`: A user-defined name to identify the account, such as "Marketing HubSpot Account" or "Development Anthropic Key." This helps distinguish it from other accounts in the same service.
-   `Account Credentials`: The authentication details (e.g., API keys or OAuth tokens) required to connect securely to the external service. Credentials can be tested or updated if they become invalid.
-   `Default Status`: An optional setting that makes the account the default choice for its service, streamlining its use in workflows.

## Types of accounts

**User-managed accounts:**

-   Configured by users with their own credentials, such as personal API keys or OAuth tokens.
-   Ideal for integrations that require team- or project-specific access.

**Clay-managed accounts:**

-   Provided by Clay and configured for public use — no individual credentials, API keys, or service contracts required.
-   These accounts bill through your workspace's actions (for platform orchestration) and data credits (for data costs) instead of your own credentials.
-   Clearly labeled in the `Connections` section, and often pre-set as default.

## Add a new integration account

To add a new account for an integration:

-   Navigate to `Settings` > `Connections`.
-   Click `+ Add connection` in the top-right corner.
-   Use the search bar to locate the service you want to integrate with.
-   Follow the on-screen instructions to authenticate and configure the connection — through an API key or by signing in to the service.
-   Name your integration account so it's easy to identify later.
-   (Optional) Set it as the default account. Enrichments using this integration will default to this account in your workspace.
-   Once completed, the account will appear under the corresponding service in the `Connections` list.

## Managing existing accounts

**Note:** Some connection management actions are restricted by role:

-   **Set as Default** is a **workspace admin–only** action — only admins see this option in the `…` menu.
-   **Reconnect** is available to the member who added the connection and to workspace admins. If you don't see a Reconnect option for a connection, it was likely added by another team member — ask a workspace admin to update the credentials.
-   **Delete** is available to the member who added the connection and to workspace admins. If you need to delete a connection that was added by someone else, ask a workspace admin.

### View your integration accounts

-   Navigate to `Settings` > `Connections`.
-   Select a service (e.g., HubSpot or Anthropic) to see all associated accounts.
-   Use the search bar to quickly locate a specific account.

### Edit your integration accounts

-   Select the service and click the `…` menu next to an account.
-   Choose `Edit` to:
    -   Update the `Key Name`.
    -   Modify or re-enter credentials.
-   Toggle `Set as Default` to make this account the default.
-   Click `Save` to apply changes.

### Rotating or updating credentials

Use **Reconnect** to replace the credentials on an existing connection — for example, to rotate an API key, swap a private key file, or update authentication details when your security team requires it. You do not need to delete or recreate the connection, or re-point individual tables or columns to a new account — the same connection is preserved, and all existing columns, workflows, and sources will automatically use the updated credentials on their next run.

> **Note:** If the new credentials have different permissions or API scopes than the original ones, some workflows may be affected. Before reconnecting, verify that the new credentials grant the same level of access as the existing ones.

> **Who can reconnect:** The Reconnect option is only available to the workspace member who originally added the connection and to workspace admins. If you don't see the `…` menu or the Reconnect option for a connection, it was added by another team member — ask a workspace admin to update the credentials on your behalf.

To rotate or update credentials:

-   Navigate to `Settings` > `Connections` and select the service.
-   Click the `…` menu next to the account and choose **Reconnect**.
-   Enter the new credentials in the modal and click **Save**.

The connection updates in place — the same connection is preserved with the new credentials. Existing data values already enriched and stored in your table rows are not affected — Reconnect does not clear or overwrite previously enriched cell values. Only actively re-running an enrichment column on existing rows would change those stored values.

### When a workspace member leaves

When a user is removed or deactivated from a workspace, their personal credentials on any connections they added are disabled. Any enrichment columns or workflows that reference those connections will stop working on their next run.

To prevent disruption, reassign their connections **before** removing them from the workspace:

1.  Navigate to `Settings` → `Connections`.
2.  Identify connections belonging to the leaving teammate.
3.  Click the `…` menu next to each connection and choose **Reconnect**.
4.  Sign in with a different active account's credentials.

Reconnect updates the connection in place — the same connection is preserved with the new credentials, and every column or workflow already referencing it will automatically use the updated credentials on its next run. You do not need to update each column individually.

> **Note:** Do not delete the connection and add a new one. Deleting a connection leaves all existing columns pointing to the deleted connection's ID — they will fail on their next run. Use Reconnect to update the credentials in place so existing columns continue to work.

### Verify connection health

If you are unsure whether a connected account is still working — for example, after a team member who set it up has left, or after a period of inactivity — you can check its status directly from Settings.

1.  Click your profile picture in the top-right and select `Settings`.
2.  In the sidebar, select the `Connections` tab.
3.  Click into the integration you want to check.
4.  Click **Verify** next to any account.

Clay tests the connection and shows a status badge:

-   **Connected** (green) — The credential is valid and the connection is working normally.
-   **Warning** (orange) — The connection is working but something may need attention, such as approaching a quota limit.
-   **Error** (red) — The credential is invalid or expired and needs to be re-authenticated.

If the status shows **Warning** or **Error**, click the badge and select **Reconnect** to re-authenticate the account.

> **Note:** Clay-managed accounts (integrations where Clay provides the API key) always show a static **Connected** badge — these are maintained by Clay and do not need manual verification.

### Testing credentials

To ensure your account credentials are valid and the integration is functioning correctly:

-   Navigate to `Settings` > `Connections`.
-   Select the service (e.g., Anthropic) to view its associated accounts.
-   Locate the account you want to test.
-   Click the `…` menu next to the account and select `Test Connection`.

### Setting default accounts

A **default account** is automatically selected for workflows or integrations where no specific account is specified. To set an account as default:

-   Navigate to `Settings` > `Connections` and select the desired service (e.g., Anthropic).
-   Locate the account you wish to set as the default.
-   Click the `…` menu next to the account, and select `Set as Default`.
-   The account will now display a `default` label to indicate its status.

**Note:** The default account is used when creating new columns and workflows going forward — it does not retroactively update existing columns or workflows. Columns already configured to use a specific connection continue to reference that connection regardless of which account is set as default. To update all existing columns to use a different account's credentials, use **Reconnect** on the connection those columns already reference (see [Rotating or updating credentials](#rotating-or-updating-credentials) above). Reconnecting updates the credentials in place so every column referencing that connection automatically uses the updated account on its next run.

**Note:** Workspace connection defaults apply per provider — there is no single setting that routes all AI usage to one API key. For Claygent columns (including those using custom MCP servers), you also need to manually select a non-Clay model (such as Claude Sonnet or GPT) in the model picker, since Claygent defaults to Clay's parallel models and does not automatically switch to a third-party model when you set a connection as default.

### Deleting accounts

-   Navigate to the service in the `Connections` section.
-   Click the `…` menu next to the account and select `Delete`.
-   Confirm the deletion.

### Clay-managed accounts

Clay-managed accounts simplify access to external services by providing pre-configured integrations that use workspace credits instead of requiring individual credentials.

For some integrations, only Clay-managed accounts are supported. For others, you will need to provide your own API key.
