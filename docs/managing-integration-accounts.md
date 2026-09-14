---
title: Managing integration accounts
description: How to add, edit, delete, and reconnect Clay integration accounts, including Clay-managed accounts and personal API key connections.
last_synced: 2026-09-14T19:04:53.334Z
---

# Managing integration accounts

Manage your Clay-managed and personal integration accounts.

Clay consolidates multiple data providers into a single platform and integrates with your tech stack through 100+ available integrations.

-   **Eliminate data procurement fatigue:** Clay-managed accounts simplify contract management with data providers, handling billing through Actions and Data Credits.
-   **Integrate with core tools:** Choose from 100+ integrations to ensure compatibility with your go-to-market system.
-   **Flexibility to bring your own API key:** Use Clay-managed accounts for quick setup or connect your own API keys at no extra cost (paid feature).

## Using Clay-managed accounts

Clay-managed accounts are pre-configured integrations that let you access data providers without individual credentials or API keys. These accounts use actions (for platform orchestration) and data credits (for data costs) to simplify access and eliminate the need for individual service contracts.

Some integrations only support Clay-managed accounts, while others let you use either Clay-managed accounts or your own API keys.

### Move existing columns to a different account

When the account behind a connection changes — someone leaves the workspace, or you're moving from a personal account to a shared integration account — you don't need to touch the columns that use it. Reconnecting a connection swaps the credentials underneath it and leaves everything pointed at it intact.

1.  Go to `Settings` → `Connections`.
2.  Find the connection you want to move.
3.  Choose `Reconnect`.
4.  Sign in with the new account's credentials.

Every column, workflow, and scheduled run tied to that connection now uses the new account. Nothing needs updating column by column.

This works because the connection itself is the thing your columns reference, and reconnecting changes only its authentication. It's the right move when you're **replacing** an account. It is not how you move work between two accounts that both already exist as their own connections in the workspace — there, the columns reference two different connections, and each has to be repointed.

## Add an integration account

To add an integration account:

1.  Click your profile picture in the top-right and select `Settings`.
2.  In the sidebar, select the `Connections` tab.
3.  Click `Add Connection` and pick the integration you want from the list.
4.  Configure your integration connection through an API key or by signing in via SSO.
5.  Name your integration account.
6.  (Optional) Set it as the default account. Enrichments using this integration will default to this account in your workspace.

## Edit an integration account

You can edit your integration account to change your API key, rename your account, or modify the default integration account.

1.  Click your profile picture in the top-right and select `Settings`.
2.  In the sidebar, select the `Connections` tab.
3.  Find the integration you want to modify and click into it.
4.  Click `...` next to the account and select `Edit`.
5.  Update the account details and save your changes.

## Delete an integration account

To delete an integration account:

1.  Click your profile picture in the top-right and select `Settings`.
2.  In the sidebar, select the `Connections` tab.
3.  Click into the integration of the account you want to delete.
4.  Click `...` next to the account and select `Delete`.
