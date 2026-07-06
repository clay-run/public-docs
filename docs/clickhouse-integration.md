---
title: ClickHouse integration
description: Connect Clay to your ClickHouse database to run insert, lookup, update, and upsert operations. Available on Enterprise plans, currently in closed Beta.
---

# ClickHouse integration

Connect Clay to your ClickHouse database to run insert, lookup, update, and upsert operations.

> **Currently in closed Beta on Enterprise plans.** To request access, reach out to your account team or contact support.

ClickHouse is a columnar database management system designed for fast analytical queries. The Clay ClickHouse integration mirrors the Snowflake integration's action set: insert, lookup, update, and upsert rows. Audiences and Big Source are not yet supported.

## Connecting to ClickHouse

When adding a ClickHouse connection in Clay, you'll need:

-   **Host** — your ClickHouse server URL, including the protocol (e.g. `https://abc123.us-east-1.aws.clickhouse.cloud`). Defaults to `https` if no protocol is specified.
-   **Port** — `8443` for ClickHouse Cloud; use the HTTPS port your self-hosted instance listens on.
-   **Username** — your ClickHouse username.
-   **Password** — your ClickHouse password.
-   **Default database** (optional) — a default database to connect to. If not specified, you'll enter it when configuring each action.

## Enriching data with ClickHouse

To add a ClickHouse action column:

1.  In a Clay table, click `Add enrichment` and search for `ClickHouse`.
2.  Select the action you want to run.
3.  Select your ClickHouse account (or click `+ Add account` to connect one).
4.  Select your database and table. Clay loads the column list from your ClickHouse instance automatically.

### `Action` Insert row

Insert a row into a ClickHouse table. Map each column to a value — leave a column blank to use its default.

**Batching:** Supports **Run in batches** mode (up to 1,000 rows per batch). Rows are grouped into a single `INSERT` statement using `JSONEachRow` format.

### `Action` Lookup row

Run a raw `SELECT` query to find a row in ClickHouse.

**Inputs**

-   **SQL query** — a `SELECT` statement, e.g. `SELECT * FROM my_table WHERE id = 1`.

**Tips**

-   **Always include `LIMIT` in your query.** The lookup returns all matching rows. Queries that can match many records can produce a response large enough to trigger a size-limit error. Adding `LIMIT 1` (or a small number) keeps each result manageable — this is especially important when **Run in Batches** is enabled, since Clay combines results from all sub-queries into a single response.

**Batching:** Supports **Run in batches** mode (up to 100 queries per batch). Clay combines sub-queries using `UNION ALL`. Include a `LIMIT` clause to cap how many rows each sub-query returns.

### `Action` Update row

Update rows in a ClickHouse table matching a `WHERE` clause. Runs as a synchronous mutation (`ALTER TABLE ... UPDATE`), which can be slow on large tables.

**Inputs**

Select a database and table; Clay loads the column list automatically. For each run, specify:

-   **Where clause** — a SQL `WHERE` condition selecting the rows to update (e.g. `WHERE id = 1`).
-   **Column values** — map each column you want to update to a new value; leave a column blank to leave it unchanged.

**Batching:** Supports **Run in batches** mode (up to 200 rows per batch). ClickHouse mutations apply in order and block until each completes, so the update action limits concurrency to 5 simultaneous requests per workspace to avoid timeouts.

### `Action` Upsert row

Insert or deduplicate a row in a ClickHouse table. Values are written using `INSERT`; deduplication is handled by the table engine. **The target table should use a `ReplacingMergeTree`-family engine** — without it, duplicate rows are not collapsed automatically.

**Batching:** Supports **Run in batches** mode (up to 1,000 rows per batch).
