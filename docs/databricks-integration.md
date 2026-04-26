---
title: Databricks integration
source_url: https://university.clay.com/docs/databricks-integration
description: Import, insert, update, upsert or look up rows in Databricks.
last_synced: 2026-04-26T01:39:51.990Z
upstream_hash: c21018070b0011eccd833efab98ec7345914cbe4c7d672ae21aacf1a360b76e3
---

# Databricks integration

Import, insert, update, upsert or look up rows in Databricks.

Databricks is a unified data and analytics platform for managing, transforming, and querying data at scale.

With this integration, you can connect to your Databricks workspace and perform SQL operations — such as importing, inserting, updating, upserting, or looking up rows — all directly from your Clay table.

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
    -   `Use static IP?`: Optional. Use a static IP when connecting to ensure that enrichments are run from a static list of IP addresses, which can be useful for allow-listing.
    -   `Workspace URL`: Your Databricks workspace URL (e.g. `https://adb-1234567890123456.7.azuredatabricks.net/`).
    -   `Client ID`: The client ID from your Databricks Service Principal.
    -   `Client secret`: The client secret from your Databricks Service Principal.
4.  Click `Authenticate` to save the connection.

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

Use this action to insert or update a row in a Databricks table using a unique identifier.

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
