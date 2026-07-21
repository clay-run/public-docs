---
title: Connections
description: Overview of the Connections settings page, where you can view, filter, manage access to, and verify every integration and connected service in your workspace.
last_synced: 2026-07-21T20:58:02.418Z
---

# Connections

Manages every integration and connected service in one place.

The `Connections` page is where your workspace manages every integration and connected service in one place — including your CRM, data warehouse, data providers, and LLM providers. From a single table you can check each connection's status, control who can use it, verify its credentials, and see exactly where it's used across your workspace.

From the `Connections` page, you can:

-   **See every connection in one table** — each row is one connection, with columns for `Provider`, `Connection name`, `Account type`, `Status`, `Resources`, `Shared with`, `Added by`, and `Date added`. `Provider`, `Connection name`, `Account type`, `Added by`, and `Date added` are sortable.
-   **Filter and search** — narrow by `Provider`, `Account type`, or `Added by`, or search by `Provider`, `Connection name`, or `Added by`.
-   **Trace usage** — open the `Resources` panel to see every workbook, table, Claygent, Signal, and more that a connection powers.
-   **Manage access** — see which people and groups can use each connection.
-   **Verify and reconnect** — re-check a connection's credentials on the spot and reconnect if needed.

## Using the Connections page

1.  Go to `Settings → Connections`.
2.  Review your connections in the table. Each row is a single connection (an "app account") — the credential Clay uses to talk to an external service like `Salesforce`, `HubSpot`, or a data provider.
3.  Use the filters at the top of the table to narrow by:
    -   `Provider`
    -   `Account type` — `User-added` or `Clay-provided`
    -   `Added by` — the user who added the connection
4.  Or search to find a connection by `Provider`, `Connection name`, or `Added by`.

**Note:** What you see depends on your role. Workspace admins see every connection in the workspace, including restricted ones they aren't personally added to. Editors see connections shared with Anyone in the workspace, restricted connections they've been added to (individually or through a group), and connections they own.

### Seeing where a connection is used

Click the resource count in the `Resources` column to open a side panel listing every resource that uses the connection. Filter the panel by `Workbooks`, `Tables`, `Functions`, `Claygents`, `Signals`, `Ads`, and `Audiences`.

### Seeing who has access

**Note:** The Shared with column and connection access controls are available on Enterprise plans.

The `Shared with` column shows the people and groups that can use a connection as an avatar stack (groups first). Click the overflow to see the full list, split into `Groups` and `Individuals`. This column shows `Anyone in the workspace` for unrestricted connections, or `Nobody added` for restricted connections that have no users or groups added yet.

To restrict a connection and control who can use it, see [Access settings for connections](https://university.clay.com/docs/access-settings-for-connections).

## Verifying and reconnecting a connection

In the `Status` column, click `Verify` to re-check a connection's credentials. The status shows `Checking`, then resolves to `Connected` or `Error` (accounts that can't be validated show `Unknown`). If a connection needs attention, click the status pill to `Reconnect`. Workspace admins also get a `Run log` for troubleshooting.

## FAQs

### What's the difference between a user-added and a Clay-provided connection?

A user-added connection is one that someone in your workspace added with their own credentials, and its owner is that user. A Clay-provided connection is provided by Clay and shared with anyone in the workspace. Use the `Account type` filter to see each.
