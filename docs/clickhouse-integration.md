---
title: ClickHouse integration
description: Import, insert, update, upsert, or look up rows in ClickHouse.
last_synced: 2026-07-01T00:00:00.000Z
---

# ClickHouse integration

Import, insert, update, upsert, or look up rows in ClickHouse.

ClickHouse is an open-source, column-oriented database management system designed for high-performance analytics on large datasets.

With this integration, you can connect to your ClickHouse instance and perform SQL operations — importing data into Clay tables, or writing enriched records back to ClickHouse — all directly from your Clay table.

> **Note:** The ClickHouse integration is currently in closed beta for Enterprise plan customers. To request access, contact your account team or reach out in [#team-enterprise-and-billing](https://clay-hq.slack.com/archives/C08K72PDRBP). Audiences and Big Source are not yet supported; this integration mirrors the Snowflake integration for regular table and enrichment actions only.

## Connecting to ClickHouse

To connect your ClickHouse account to Clay:

1.  In the home sidebar, click `Settings` → `Connections`.
2.  Click `Add connection` and search for `ClickHouse`.
3.  Fill in the following fields:
    -   **Host**: Your ClickHouse host URL (e.g. `https://abc123.us-east-1.aws.clickhouse.cloud`). Defaults to HTTPS if no protocol is specified.
    -   **Port**: The port for your ClickHouse instance (use `8443` for ClickHouse Cloud).
    -   **Username**: Your ClickHouse username.
    -   **Password**: Your ClickHouse password.
    -   **Default database** (optional): The database to use by default. If not specified, you'll be prompted to enter it when setting up an action.
4.  Click `Authenticate` to save the connection.

## Setting up the ClickHouse integration

1.  While in a Clay table, click `Add enrichment` and search for `ClickHouse`.
2.  Under `Integrations`, select one of the ClickHouse options.
3.  In the modal, select your ClickHouse account.
    -   If you haven't already connected your ClickHouse account, click `+ Add account` and complete the connection setup above.

## Actions

### `Source` Import from ClickHouse

Pull data from a ClickHouse table into a Clay table using a SQL query.

**Inputs**

-   **SQL query**: A `SELECT` query specifying the data to import. Only `SELECT` queries are allowed.

### `Action` Insert row

Insert a row into a ClickHouse database.

**Inputs**

-   **ClickHouse account** (includes host, port, and optionally the default database)
-   **Table**: The target table to insert into.
-   **Column mapping**: Map each ClickHouse column to a value. Columns are surfaced dynamically based on the selected table. Leave a column blank to use its default value.

**Batching**

The Insert row action supports **Run in batches** mode with a maximum batch size of 1,000 rows.

### `Action` Lookup row

Check if a row exists in your ClickHouse database using a raw SQL query.

**Inputs**

-   **ClickHouse account**
-   **SQL query**: The raw `SELECT` query to run.

**Batching**

The Lookup row action supports **Run in batches** mode with a maximum batch size of 100 rows.

### `Action` Update row

Update a row in a ClickHouse database.

**Inputs**

-   **ClickHouse account**
-   **Table**: The target table to update.
-   **Column mapping**: Map ClickHouse columns to updated values. Columns are surfaced dynamically based on the selected table.

**Batching**

The Update row action supports **Run in batches** mode with a maximum batch size of 1,000 rows.

### `Action` Upsert row

Create or update a row in a ClickHouse database.

**Inputs**

-   **ClickHouse account**
-   **Table**: The target table.
-   **Column mapping**: Map ClickHouse columns to values. Columns are surfaced dynamically based on the selected table.

**Batching**

The Upsert row action supports **Run in batches** mode with a maximum batch size of 1,000 rows.
