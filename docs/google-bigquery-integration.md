---
title: Google BigQuery integration
source_url: https://university.clay.com/docs/google-bigquery-integration
last_synced: 2026-04-26T01:40:03.104Z
upstream_hash: c455f35299a4375d4e63f5826a51ef966f5775962999615cb2c5157ed5ef0abc
---

# Google BigQuery integration

Import records from BigQuery into Clay using SQL queries, and send enriched data back by inserting, looking up, updating, or upserting rows in your BigQuery tables.

Google BigQuery is a fully managed, serverless data warehouse built for large-scale analytics. With this integration, you can import records from BigQuery into Clay using SQL queries, and send enriched data back by inserting, looking up, updating, or upserting rows in your BigQuery tables.

## Create a table with Google BigQuery

1.  In a workbook, click `+ Add` at the bottom.
2.  Search for `Google BigQuery` and select it from the results.
3.  In the modal, you will be asked to `Select Google BigQuery account`.
    -   If you haven't connected BigQuery yet, click `+ Add account` and upload your service account JSON key file. Follow the prompts to assign the required IAM roles, or use [Google's service account docs](https://developers.google.com/workspace/guides/create-credentials#service-account).

### `Source` Import data from BigQuery

Imports records from Google BigQuery into a Clay table using a custom SQL query.

**Inputs**

-   SQL query: A `SELECT` or `WITH` statement to run against your BigQuery project. Use standard SQL syntax (e.g., `SELECT * FROM \\`project.dataset.table `WHERE created_at > "2024-01-01"`).
-   Unique identifier: The column to use for row deduplication. This field appears as a dropdown after you enter a valid query — select a column that contains unique values for each record.

**Note:** The Import Data from BigQuery source supports up to 50,000 rows per run.

## Enrich data with Google BigQuery

1.  While in a Clay table, click `Add enrichment` and search for `Google BigQuery`.
2.  Under `Integrations`, select one of the options.
3.  In the modal, you will be asked to `Select Google BigQuery account`.
    -   If you haven't already connected your Google BigQuery account, click `+ Add account` and upload your service account JSON key file.

### `Action` Insert row into BigQuery

Inserts a new row into a Google BigQuery table using streaming inserts for high throughput.

**Inputs**

Required:

-   Dataset ID: The BigQuery dataset to insert into. Displays as a dropdown populated from your connected account.
-   Table ID: The table to insert into. Displays as a dropdown populated from the selected dataset.

Optional:

-   Column mapping: Map Clay values to each table column. Columns are dynamically loaded from the selected table's schema. Columns marked `Required` in BigQuery will be flagged as required in the mapping.

**Outputs**

-   Inserted Count: The number of rows successfully inserted.

### `Action` Lookup row in BigQuery

Looks up rows in a Google BigQuery table by matching one or more column values.

**Inputs**

Required:

-   Dataset ID: The BigQuery dataset to search. Displays as a dropdown populated from your connected account.
-   Table ID: The table to search. Displays as a dropdown populated from the selected dataset.
-   Lookup column(s): The column(s) to filter by. Select multiple columns to combine search conditions.
-   Search operator: (Required if multiple lookup columns are selected.) Choose `AND` to require all conditions to match, or `OR` to require at least one to match.
-   \[Column name\] value: The value to search for in each selected lookup column. One input field appears per selected column.

Optional:

-   Returned fields: Select which columns to return in the output. Leave empty to return all columns.
-   Limit: The maximum number of matching rows to return. Defaults to 10; maximum is 1,000.

**Outputs**

-   Row data: Returns the column values of matching rows, dynamically based on the selected table's schema and the `Returned fields` configuration.

### `Action` Update row in BigQuery

Updates rows in a Google BigQuery table that match a specified WHERE clause.

**Inputs**

Required:

-   Dataset ID: The BigQuery dataset containing the table. Displays as a dropdown populated from your connected account.
-   Table ID: The table to update. Displays as a dropdown populated from the selected dataset.
-   WHERE clause: The filter condition identifying rows to update (e.g., `WHERE email = "john@example.com"`). Must begin with the `WHERE` keyword.

Optional:

-   Column mapping: The columns to update and their new values. Columns are dynamically loaded from the selected table. Leave a field empty to keep the existing value in that column.

**Outputs**

This action does not return output values.

### `Action` Upsert row in BigQuery

Inserts a new row or updates an existing row in a Google BigQuery table using a `MERGE` statement.

**Inputs**

Required:

-   Dataset ID: The BigQuery dataset to upsert into. Displays as a dropdown populated from your connected account.
-   Table ID: The table to upsert into. Displays as a dropdown populated from the selected dataset.
-   Lookup field: The column to match on when determining whether to insert a new row or update an existing one.

Optional:

-   Column mapping: Map Clay values to each table column. Columns are dynamically loaded from the selected table.

**Outputs**

This action does not return output values.

### Run settings

-   Auto-update: Recommended for keeping BigQuery data in sync as new rows are added or updated in your Clay table.
-   Only run if: The enrichment will only run if conditions are met. ([Learn more about conditional formulas](https://university.clay.com/docs/conditional-formulas)).
