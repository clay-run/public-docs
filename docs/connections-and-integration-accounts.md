---
title: Connections and integration accounts
description: Add, edit, test, and delete integration accounts in Clay's Connections settings, verify connection status (including why it resets to Verify after a refresh), view where each connection is used, and set default accounts for your workspace.
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
-   Click `Create` in the top-right corner. The `Connect an account` modal opens.
-   Use the `Search` field in the `Connect an account` modal to locate the service you want to integrate with.
-   Follow the on-screen instructions to authenticate and configure the connection — through an API key or by signing in to the service.
-   Name your integration account so it's easy to identify later.
-   (Optional) Set it as the default account. Enrichments using this integration will default to this account in your workspace.
-   Once completed, the account will appear under the corresponding service in the `Connections` list.

### Why an integration doesn't show up on the Connections page

The `Settings` > `Connections` page only lists connections your workspace has already added. An integration you haven't connected yet — for example, HubSpot or Salesloft — doesn't appear in the list until you add an account for it with the `Create` button.

The search bar on the `Settings` > `Connections` page (next to the `Create` button) only filters connections your workspace has already added. It does not search the integrations available to connect. If you search for an integration you haven't connected yet — for example, typing "salesloft" before adding a Salesloft API key — the Connections page shows **No connections match your filters** and "Try adjusting your search or filters." This doesn't mean the integration is unavailable.

To find and add an integration you haven't connected yet:

1.  On the `Settings` > `Connections` page, click `Create` in the top-right corner.
2.  In the `Connect an account` modal, type the integration's name (for example, "Salesloft") into the `Search` field.
3.  Select the integration and follow the prompts to authenticate — for API key integrations, paste your API key and name the account.
4.  Save the account. It now appears in the `Connections` list, and searching the Connections page for it will return it.

You can also add an account from inside a table: open an action for that integration, go to the `Account` section in the action's sidebar, open the account dropdown, and select `Add account`. Accounts added this way are saved to your workspace, appear in the `Connections` list, and can be reused across every action for that integration.

## Managing existing accounts

**Note:** Some connection management actions are restricted by role:

-   **Set as Default** is a **workspace admin–only** action — only admins see this option in the `…` menu.
-   **Reconnect** is available to the member who added the connection and to workspace admins. If you don't see a Reconnect option for a connection, it was likely added by another team member — ask a workspace admin to update the credentials.
-   **Revoke** (deletes the connection) is available to the member who added the connection and to workspace admins. If you need to delete a connection that was added by someone else, ask a workspace admin.

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

### Viewing resources that use a connection

The **Resources** column on the Connections table shows how many resources — workbooks, tables, functions, Claygents, Audiences, Signals, Ads, and workflows — reference each connection. A connection that no resource uses shows `—` in the Resources column. To see the full list for a specific connection:

1.  Navigate to `Settings` > `Connections`.
2.  Find the connection you want to inspect. You can type the provider name (for example, "hubspot") into the search bar to narrow the list.
3.  Click the count in the **Resources** column, or click the `…` menu next to the account and select **View resources**. The **View resources** option only appears when the connection is used by at least one resource.

A panel opens with the connection's name at the top and the message "This connection is used in the resources below." It lists every workbook, table, function, Claygent, Audience, Signal, Ad, and workflow that uses that connection. Expand a workbook to see its tables, and expand a table to see the specific columns and sources in it that use the connection — for example, a HubSpot `Create object` column or an `Import objects from HubSpot` source. Use the **Resource type** filter (default: **All resources**) to narrow the list to Workbooks, Tables, Functions, Ads, Audiences, Claygents, Signals, or Workflows. Each resource row shows an external-link icon — click it to open that resource in a new tab while keeping the panel open.

Use this before rotating credentials, reconnecting with new credentials, or removing a connection — it shows exactly which parts of your workspace will be affected. It is also the recommended first step when a team member who owns connections is leaving and you need to identify which connections to update before their account is deactivated (see the FAQ below).

### Rotating or updating credentials

Use **Reconnect** to replace the credentials on an existing connection — for example, to rotate an API key, swap a private key file, or update authentication details when your security team requires it. You do not need to delete or recreate the connection, or re-point individual tables or columns to a new account — the same connection is preserved, and all existing columns, workflows, and sources will automatically use the updated credentials on their next run.

> **Note:** If the new credentials have different permissions or API scopes than the original ones, some workflows may be affected. Before reconnecting, verify that the new credentials grant the same level of access as the existing ones.

> **Who can reconnect:** The Reconnect option is only available to the workspace member who originally added the connection and to workspace admins. If you don't see the `…` menu or the Reconnect option for a connection, it was added by another team member — ask a workspace admin to update the credentials on your behalf.

To rotate or update credentials:

-   Navigate to `Settings` > `Connections` and select the service.
-   Click the `…` menu next to the account and choose **Reconnect**.
-   Enter the new credentials in the modal and click **Save**.

The connection updates in place — the same connection is preserved with the new credentials. Existing data values already enriched and stored in your table rows are not affected — Reconnect does not clear or overwrite previously enriched cell values. Only actively re-running an enrichment column on existing rows would change those stored values.

### Verify connection health

If you are unsure whether a connected account is still working — for example, after a team member who set it up has left, or after a period of inactivity — you can check its status directly from Settings.

1.  Click your profile picture in the top-right and select `Settings`.
2.  In the sidebar, select the `Connections` tab.
3.  Click into the integration you want to check.
4.  Click **Verify** next to any account, if the button appears. Some integration types do not support automated verification and will show a **View in {provider}** badge instead of a Verify button.

Clay tests the connection and shows a status badge:

-   **Connected** (green) — The credential is valid and the connection is working normally.
-   **Warning** (orange) — The connection is working but something may need attention, such as approaching a quota limit.
-   **Error** (red) — The credential is invalid or expired and needs to be re-authenticated.
-   **View in {provider}** (neutral) — The connection type does not support automated health verification. Clay cannot test whether this integration's credential is still valid. Hovering over the badge shows: *"Status for this connection is only available in {provider name}."* This does not mean the connection is broken — it means no automated check is available for this integration type.

If the status shows **Warning** or **Error**, click the badge and select **Reconnect** to re-authenticate the account.

> **Note:** Clay-managed accounts (integrations where Clay provides the API key) always show a static **Connected** badge — these are maintained by Clay and do not need manual verification.

### Why a connection shows Verify again after you refresh the page

On the `Settings` > `Connections` page, the **Status** column for an account you added with your own API key (for example, your own Anthropic API key) shows a **Verify** button every time the page loads. This is expected. A **Connected** result from clicking **Verify** only lasts until you refresh or leave the page — Clay does not save the verification result, so after a browser refresh the account goes back to showing **Verify**.

Seeing **Verify** after a refresh does not mean your API key was lost, wasn't saved, or is disconnected. The key is still saved on the connection, and any columns that use that account keep using it. You do not need to reconnect or re-enter the key.

To confirm the key still works at any time:

1.  Navigate to `Settings` > `Connections` and select the service (for example, Anthropic).
2.  Click **Verify** next to the account. The status shows **Checking** while Clay tests the key.
3.  You'll see **Connected** if the key is valid. If you see **Error**, click the `…` menu next to the account and choose **Reconnect** to enter a new key (see [Rotating or updating credentials](#rotating-or-updating-credentials)).

Clay-managed accounts (for example, the Clay-managed Anthropic account) always show **Connected** and never show a **Verify** button, so it's normal for a Clay-managed account and your own key to show different statuses side by side after a refresh.

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
-   Click the `…` menu next to the account and select `Revoke`.
-   Confirm the deletion.

Revoke is how you delete or disconnect a connection in Clay. It isn't available on Clay-managed accounts.

> **Important:** If the connection you delete is referenced by existing columns, sources, or workflows, those items will stop working — they still point to the deleted connection's ID and will fail on their next run. **There is no bulk way to reassign existing columns to a new connection.** You would need to open each affected column individually and select the new connection from the **Account** dropdown.
>
> **Revoking a connection also removes its Audiences imports.** If an Audience imports records from a CRM such as Salesforce through this connection, revoking the connection permanently deletes those Audience imports and their field mappings. They don't come back if you add a new connection later — you would have to set up each import and field mapping again by hand.
>
> To avoid this, **use Reconnect instead of deleting and recreating the connection when rotating an API key or changing which user the connection signs in as.** Reconnecting updates the credentials in place, so every column and workflow that references that connection automatically uses the updated key — no column-by-column work needed. See [Rotating or updating credentials](#rotating-or-updating-credentials) above.

### Clay-managed accounts

Clay-managed accounts simplify access to external services by providing pre-configured integrations that use workspace credits instead of requiring individual credentials.

For some integrations, only Clay-managed accounts are supported. For others, you will need to provide your own API key.

## FAQs

**What should I do when a team member who owns connections is leaving?**

Before the member's account is deactivated, a workspace admin should:

1.  Navigate to `Settings` > `Connections` and search or filter by the departing member's name (use the **Added by** column to identify connections they own).
2.  Click `…` > **View resources** for each of their connections to see which tables, workbooks, functions, Claygents, Audiences, Signals, Ads, and workflows depend on it.
3.  Click `…` > **Reconnect** to re-authenticate using a service account or another team member's credentials. All tables and workflows that reference that connection will automatically use the new credentials on their next run — you do not need to update each table individually.

Don't revoke the departing member's connection and create a new one in its place. Clay has no bulk way to move resources from one connection to another, so you would have to re-point every table column to the new connection one at a time. Revoking also permanently deletes any Audiences imports and field mappings that use the connection (see [Deleting accounts](#deleting-accounts)).

Once the member's account is deactivated, their personal credentials are disabled. Any connections that were not reconnected to new credentials will stop working.

**How do I switch a Salesforce connection from a departing user to an integration user without breaking my Audiences syncs?**

Use **Reconnect** on the existing Salesforce connection and sign in as the new user. The connection stays the same in Clay; only the Salesforce user behind it changes. Your Audience imports, field mappings, tables and workflows that use the connection keep working and use the new user's credentials on their next run.

1.  Open an incognito or private browser window, so the departing user's Salesforce login isn't picked up by mistake.
2.  Log into Clay in that window and go to `Settings` > `Connections`. Search for `Salesforce` to find the departing user's connection.
3.  Click `…` > **Reconnect** and, in the Salesforce sign-in popup, log in as the new user (for example, your integration user).
4.  Optionally, click `…` > `Edit` to rename the connection so the name matches the new user.

Do this before the departing user's Salesforce account is deactivated. The new user should have API access and the same object and field permissions as the original user. Otherwise, imports or updates that relied on those permissions may fail. For more on signing in as a specific Salesforce user, see [How do I connect to Salesforce as a specific user](./salesforce-integration-faqs.md#how-do-i-connect-to-salesforce-as-a-specific-user-such-as-an-integration-user-using-user-sign-in).
