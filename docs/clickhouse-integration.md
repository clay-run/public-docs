---
title: ClickHouse integration
description: Import data from ClickHouse into Clay tables using SQL queries, and send
  enriched data back by inserting, looking up, updating, or upserting rows in your
  ClickHouse database.
last_synced: 2026-07-03T00:00:00.000Z
---

# ClickHouse integration

Import data from ClickHouse into Clay tables using SQL queries, and send enriched data back by inserting, looking up, updating, or upserting rows in your ClickHouse database.

ClickHouse is an open-source column-oriented database built for real-time analytics. This integration mirrors Clay's Snowflake integration: you can pull records into a Clay table using a SQL query, and write enriched data back to your ClickHouse database.

**The ClickHouse integration requires an Enterprise plan.** The Import from ClickHouse source is available to all Enterprise workspaces. The write and lookup actions (Insert row, Lookup row, Update row, and Upsert row) are currently in closed beta for select customers.

> **Write and lookup actions are in closed beta.** To request access, contact your account team or reach out to [support@clay.com](mailto:support@clay.com).

## Connecting to ClickHouse

1.  In the home sidebar, click `Settings` → `Connections`.
2.  Click `Add connection` and search for `ClickHouse`.
3.  Fill in the connection fields:
    -   **Host**: Your ClickHouse host URL (e.g. `https://abc123.us-east-1.aws.clickhouse.cloud`). Defaults to HTTPS if no protocol is specified.
    -   **Port**: Your ClickHouse port. Use `8443` for ClickHouse Cloud.
    -   **Username**: Your ClickHouse username.
    -   **Password**: Your ClickHouse password.
    -   **Default database** (optional): A default database for this connection. If not specified, you will choose the database per action.

## Creating a table with ClickHouse

1.  In a workbook, click `+ Add` at the bottom.
2.  Search for `ClickHouse` and select it from the results.
3.  In the modal, select your ClickHouse account.
    -   If you haven't connected your ClickHouse account yet, click `+ Add account` and fill in the connection fields above.

### `Source` Import from ClickHouse

Pull data from a ClickHouse table into Clay using a SQL SELECT query.

**Inputs**

-   **SQL query**: The raw SELECT query to run (e.g. `SELECT * FROM my_table LIMIT 100`). A deterministic ordering is applied automatically for pagination. Only SELECT queries are accepted.
-   **Unique identifier**: A column from the query results that is unique for each row. Appears as a dropdown after you enter a valid query — select the column that uniquely identifies each record.

## Enriching data with ClickHouse

> The following actions are in closed beta. Contact your account team or [support@clay.com](mailto:support@clay.com) to request access.

1.  While in a Clay table, click `Add enrichment` and search for `ClickHouse`.
2.  Under `Integrations`, select one of the ClickHouse options.
3.  In the modal, select your ClickHouse account.

### `Action` Insert row

Insert a row into a ClickHouse database.

**Inputs**

-   **Auth fields**: Select the database and table to insert into. Databases and tables load as dropdowns from your connected account.
-   **Column mapping** (optional): Map each ClickHouse column to a value to insert. Leave a column blank to use its default.

### `Action` Lookup row

Check if a row exists in your ClickHouse database using a SQL SELECT query.

**Inputs**

-   **SQL query**: The raw SELECT query to run. Always include a `LIMIT` clause to cap results and avoid response size errors.

### `Action` Update row

Update rows in a ClickHouse database using a WHERE clause.

**Inputs**

-   **Auth fields**: Select the database and table to update.
-   **Column mapping**: Includes a required **Where clause** field (a SQL WHERE expression selecting the rows to update, e.g. `WHERE id = 1`) and one input per column for the new values. Leave a column blank to leave it unchanged.

### `Action` Upsert row

Insert or replace a row in a ClickHouse database. Deduplication applies if the table's storage engine supports it.

**Inputs**

-   **Auth fields**: Select the database and table to upsert into.
-   **Column mapping** (optional): Map each ClickHouse column to a value to write. Leave a column blank to use its default.

**Note:** Upsert behavior depends on your table's storage engine. Tables using `ReplacingMergeTree` or similar deduplicating engines will collapse duplicate rows on merge. Plain `MergeTree` or log-family tables do not deduplicate — this action will insert a new row every run. Clay surfaces a warning if the selected table's engine does not support deduplication.

### Run settings

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

## Limitations

-   **No Audiences support:** ClickHouse cannot be used as a source or destination in Clay Audiences.
-   **No Big Source:** ClickHouse is not available as an enterprise Big Source pipeline.
