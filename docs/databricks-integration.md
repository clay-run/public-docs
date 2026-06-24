---
title: Databricks integration
description: Import, insert, update, upsert or look up rows in Databricks.
last_synced: 2026-04-26T01:39:51.990Z
---

# Databricks integration

Import, insert, update, upsert or look up rows in Databricks.

Databricks is a unified data and analytics platform for managing, transforming, and querying data at scale.

With this integration, you can connect to your Databricks workspace and perform SQL operations — such as importing, inserting, updating, upserting, or looking up rows — all directly from your Clay table.

> **Note:** The Databricks integration is currently available to Enterprise plan customers enrolled in the beta. Contact your account team or [support](https://www.clay.com/support) to request access.

## Connecting to Databricks

Clay supports two methods for authenticating your Databricks account. You can choose the one that fits your organization's setup when adding a new connection or when reconnecting an existing one.

-   **Service Principal** — the recommended method. You connect via OAuth M2M (machine-to-machine) with a Service Principal for secure, server-to-server authentication.
-   **Personal Access Token** — a simpler method using a personal access token. No OAuth configuration is required.

### Service Principal

Connect to Databricks using OAuth M2M with a Service Principal for secure, server-to-server access.

1.  In the home sidebar, click `Settings` → `Connections`.
2.  Click `Add connection` and search for `Databricks`.
3.  Under `Service Principal`, fill in the following fields:
    -   `Name your connection`: A descriptive name for this connection.
    -   `Workspace URL`: Your Databricks workspace URL (e.g. `https://adb-1234567890123456.7.azuredatabricks.net/`).
    -   `Client ID`: The client ID from your Databricks Service Principal.
    -   `Client secret`: The client secret from your Databricks Service Principal.
4.  Click `Authenticate` to save the connection.

**Static IP:** Databricks connections always route through Clay's fixed IP addresses. If your Databricks workspace requires IP allowlisting, contact [Clay support](https://www.clay.com/support) for the current IP list.

### Personal Access Token

Connect to Databricks using a Personal Access Token.

1.  In the home sidebar, click `Settings` → `Connections`.
2.  Click `Add connection` and search for `Databricks`.
3.  Under `Personal Access Token`, complete the authentication flow.
    -   You'll need to generate a Personal Access Token in your Databricks workspace. See [Databricks documentation](https://docs.databricks.com/aws/en/dev-tools/auth/pat) for instructions.

## Setting up the Databricks integration

1.  While in a Clay table, click `Add enrichment` and search for Databricks.
2.  Under `Integrations`, select one of the Databricks options.
3.  In the modal, you will be asked to `Select Databricks account`.
    -   If you haven't already connected your Databricks account, click `+ Add account` and go through authentication.

## Using the Databricks integration

### Pushing enrichment data to Databricks

To push enriched records from a Clay table into your Databricks instance, use one of the write actions below.

-   **Upsert row** (recommended for most export workflows) — updates an existing record if a match is found on the unique key column, or inserts a new row if no match exists. This is the safest default for pushing data out of Clay because it handles both new and existing records without creating duplicates.
-   **Insert row** — inserts a new row. Use this when you are certain the record does not already exist in your Databricks table.
-   **Update row** — updates rows matching a SQL WHERE clause. Use this when you only want to modify records that already exist.

### `Source` Import from Databricks

Use this action to pull data from a Databricks table into Clay.

**Inputs**

-   **Databricks SQL warehouse**
-   **SQL query**

### `Action` Lookup row

Use this action to check if a row exists in a Databricks table.

**Inputs**

-   **Databricks SQL warehouse**
-   **SQL query**

### `Action` Insert row

Use this action to insert a new row into a Databricks table.

**Inputs**

-   **Databricks SQL warehouse**
-   **Databricks catalog**
-   **Databricks schema**
-   **Databricks table**
-   **Column values to insert**

### `Action` Update row

Use this action to update existing rows in a Databricks table.

**Inputs**

-   **Databricks SQL warehouse**
-   **Databricks catalog**
-   **Databricks schema**
-   **Databricks table**
-   **WHERE clause**
-   **Column values to update**

### `Action` Upsert row

Use this action to insert or update a row in a Databricks table using a unique identifier. If a record matching the unique key column already exists, it will be updated; if no match is found, a new row will be inserted.

**Inputs**

-   **Databricks SQL warehouse**
-   **Databricks catalog**
-   **Databricks schema**
-   **Databricks table**
-   **Unique key column**
-   **Column values to insert or update**

**Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))
