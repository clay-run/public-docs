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

### Closed-loop workflow: import, enrich, and write back to Databricks

Once your Databricks source is connected, you can build a fully automated loop: Databricks imports data into Clay, Clay enriches each row, and the Upsert Row action pushes the results back to your Databricks table — no webhooks required.

1.  **Schedule your source.** Open the source column settings and configure a schedule so Clay pulls fresh rows from Databricks automatically. See [scheduled sources](scheduled-sources.md) for details.
2.  **Add enrichment columns.** For each piece of data you want to add — such as employee count or company details — add an enrichment column and map its required input to the corresponding Clay column (for example, map the enrichment's domain input to the column containing your `website_domain` values).
3.  **Leave table auto-run on.** Auto-run is on by default, so every new row added by the Databricks source automatically triggers your enrichment columns as it arrives. See [auto-run](auto-run.md) for more on how this works.
4.  **Gate each enrichment with "Only run if."** Add an `Only run if` condition to each enrichment column — for example, `website_domain is not empty and Employee Count is empty` — so enrichment fires only when its input exists and the result has not already been filled in. This prevents re-runs and controls credit spend.
5.  **Add a Databricks Upsert Row action as the final column.** Select the destination table, set the `Lookup matching field` to the Databricks column that uniquely identifies each record (such as `website_domain`), and map each enrichment result to its destination Databricks column in the Column mapping section. See [how column mapping works](#how-column-mapping-works) below.
6.  **Keep auto-run on for the Upsert Row action.** With auto-run enabled on the action column, every enriched row writes back to Databricks automatically.

The result: Databricks sends rows to Clay, Clay enriches each row on arrival, and the Upsert Row action pushes the results straight back to your Databricks output table.

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
-   **Lookup matching field**
-   **Column mapping (Table Columns)**

#### How column mapping works

After you select the Databricks catalog, schema, and table, the action loads your table's column schema. The setup panel has two parts:

-   **Lookup matching field** — a dropdown listing your Databricks table's columns. Select the column that acts as the unique key for matching (for example, `website_domain`). The action uses this column name to decide whether to update an existing row or insert a new one. If no field is selected, the action will fail with a "Lookup field value missing" error.
-   **Column mapping (Table Columns)** — each Databricks column appears as a separate input field. Map each field to the Clay column that holds the value you want to write. **Only columns you explicitly map here are written to Databricks.** You must map at least one column. The lookup field column itself must also be mapped here so the action has a value to match on for each row.

**Example:** To write enriched employee count data back to a `headcount` column in Databricks while matching on `website_domain`:

1.  Set `Lookup matching field` → `website_domain`.
2.  In Column mapping, map `website_domain` to the Clay column containing domain values (so the match key has a value for every row).
3.  In Column mapping, map `headcount` to the Clay enrichment column containing the employee count result.

**Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

## Troubleshooting

### "Missing column data" error on Upsert Row

The error `Missing input: Missing column data` on a row means the action has no column values to write — either because no columns are mapped in the Column mapping section, or because all mapped Clay columns are empty for that row.

**To fix:**

1.  Open the Upsert Row action. Check that at least one column is mapped in the Column mapping (Table Columns) section. If no column fields appear, click **Refresh fields** to reload the table schema from Databricks.
2.  Make sure the lookup field column is mapped in the Column mapping section in addition to being selected in the `Lookup matching field` dropdown — the dropdown sets the column *name* used for matching, but the row *value* for that column must also be provided through the mapping.
3.  Verify that the Clay columns you've mapped have values for the affected rows. If an enrichment returned no result for a row, that cell will be empty and contribute nothing to the write.
4.  Add an **Only run if** condition to the Upsert Row action column so it fires only when the enrichment columns you're mapping have values (for example, `Employee Count is not empty`). This prevents the action from attempting to write rows where enrichment did not return results.
