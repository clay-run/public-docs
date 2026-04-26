---
title: Postgres integration overview
source_url: https://university.clay.com/docs/postgres-integration-overview
last_synced: 2026-04-26T01:40:29.644Z
upstream_hash: 84fdebd03ab3e6a3c952e86ce50f946ba24cb223bd0ec0cbd2a432189fca4830
---

# Postgres integration overview

Open-source relational database for reliable data management and scalable solutions.

## PostgreSQL Overview

PostgreSQL is a powerful, open-source relational database system.

Within Clay you can efficiently query your Postgres SQL database to check for the existence of specific rows using the Lookup Row action.

## Setting up PostgreSQL and Clay integration

To set up the PostgreSQL integration, connect your PostgreSQL account by signing in the **Settings > Connections** or via the integration panel for PostgreSQL.

## **Available Actions with the PostgreSQL**

### `Action` Lookup Row in PostgreSQL

Use this action to check if a specific row exists in your Postgres SQL database.

**Setup Inputs**

-   **SQL Query**: Enter the raw SELECT SQL query to run.
-   **Host IP Address**: Provide the public IP address of your PostgreSQL database (localhost is not valid).
-   **Port**: Enter the port number used to connect to your PostgreSQL database.
-   **Database Name**: Specify the name of the database to query.
-   **Schema** (Optional): Provide the schema containing the tables you’ll query. Leave blank if unsure.
