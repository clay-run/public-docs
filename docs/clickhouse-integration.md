---
title: ClickHouse integration
description: Connect Clay to your ClickHouse database to import data and run insert, lookup, update, and upsert operations. Available on Enterprise plans, currently in closed Beta.
---

# ClickHouse integration

Connect Clay to your ClickHouse database to import data and run insert, lookup, update, and upsert operations.

> **Currently in closed Beta on Enterprise plans.** To request access, reach out to your account team or contact support.

ClickHouse is a columnar database management system designed for fast analytical queries. Clay's ClickHouse integration mirrors the Snowflake integration: you can use ClickHouse as a source to pull data into a table, or run row-level actions (insert, lookup, update, upsert) as enrichment columns. Audiences and Big Source are not yet supported.

## Connecting to ClickHouse

When adding a ClickHouse connection in Clay, you'll need:

-   **Host** — your ClickHouse server URL, including the protocol (e.g. `https://abc123.us-east-1.aws.clickhouse.cloud`). Defaults to `https` if no protocol is specified.
-   **Port** — `8443` for ClickHouse Cloud; use the port your self-hosted instance listens on for HTTPS.
-   **Username** — your ClickHouse username.
-   **Password** — your ClickHouse password.
-   **Default database** (optional) — a default database to connect to. If not specified, you'll enter it when setting up each action.

## Creating a table with ClickHouse

### `Source` Import from ClickHouse

Pull data from a ClickHouse table into Clay using a SQL `SELECT` query.

**Inputs**

-   **SQL query** — a `SELECT` statement defining the data to import (e.g. `SELECT * FROM my_table LIMIT 100`). A deterministic ordering is applied automatically for pagination.
-   **Unique identifier** — choose a column from your query result to use as the unique row identifier. Clay uses this to deduplicate records across imports.

To set up an Import from ClickHouse source:

1.  In a workbook, click `+ Add` at the bottom.
2.  Search for `ClickHouse` and select **Import from ClickHouse**.
3.  Select your ClickHouse account (or click `+ Add account` to connect one).
4.  Enter your SQL query and select a unique identifier column.

## Enriching data with ClickHouse

To add a ClickHouse action column:

1.  In a Clay table, click `Add enrichment` and search for `ClickHouse`.
2.  Select the action you want to run.
3.  Select your ClickHouse account (or click `+ Add account` to connect one).

### `Action` Insert row

Insert a row into a ClickHouse table. Column values are mapped individually — select a table and Clay loads the column list from your database automatically.

**Batching:** Supports **Run in batches** mode (up to 1,000 rows per batch). Rows are grouped into a single `INSERT` statement using `JSONEachRow` format.

### `Action` Lookup row

Run a raw `SELECT` query to check whether a row exists in ClickHouse.

**Inputs**

-   **SQL query** — a `SELECT` statement, e.g. `SELECT * FROM my_table WHERE id = 1`.

**Batching:** Supports **Run in batches** mode (up to 100 queries per batch). Clay combines sub-queries using `UNION ALL`. If any sub-query returns many rows, the combined result can exceed a backend size limit — include a `LIMIT` clause to keep each sub-query result small.

### `Action` Update row

Update rows in a ClickHouse table matching a `WHERE` clause. Runs as a synchronous mutation (`ALTER TABLE ... UPDATE`), which can be slow on large tables.

**Inputs**

Select a database and table. Clay loads the column list from your database automatically. For each action run, specify:

-   **Where clause** — a SQL `WHERE` condition selecting the rows to update (e.g. `WHERE id = 1`).
-   **Column values** — map each column you want to update to a new value; leave a column blank to leave it unchanged.

**Batching:** Supports **Run in batches** mode (up to 200 rows per batch). Because ClickHouse mutations apply in order and block until each completes, concurrent updates can queue up and time out — the update action limits concurrency to 5 simultaneous requests per workspace.

### `Action` Upsert row

Insert or deduplicate a row in a ClickHouse table. Values are written using `INSERT`; deduplication is handled by the table engine. **The target table should use a `ReplacingMergeTree`-family engine** — without it, duplicate rows are not collapsed automatically.

**Batching:** Supports **Run in batches** mode (up to 1,000 rows per batch).
