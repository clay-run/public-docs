---
title: Managing integration accounts
description: Manage your Clay-managed and personal integration accounts, including how to add, edit, delete, and verify the health of connections.
last_synced: 2026-04-26T01:40:19.453Z
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

## Add an integration account

To add an integration account:

1.  Click your profile picture in the top-right and select `Settings`.
2.  In the sidebar, select the `Connections` tab.
3.  Click `Add Connection` and pick the integration you want from the list.
4.  Configure your integration connection through an API key or by signing in via SSO.
5.  Name your integration account.
6.  (Optional) Set it as the default account. Enrichments using this integration will default to this account in your workspace.

## Verify connection health

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
