---
title: Auto-delete in tables
source_url: https://university.clay.com/docs/auto-delete
description: Efficiently process and enrich large volumes of data.
last_synced: 2026-04-26T01:39:41.622Z
upstream_hash: fe7982619dad45bf19ff67b63bece805dfcd37d841b2ed6053e3827ef9a09387
---

# Auto-delete in tables

Efficiently process and enrich large volumes of data.

**Note:** This is a feature available to users on the Enterprise Plan.

Auto-delete is a powerful feature designed to help you process and enrich large volumes of data efficiently. It allows you to bypass the standard row limit by automatically processing incoming data, enriching it, and then forwarding it to a designated destination before deleting the original entries from the table. This ensures your tables remain manageable while continuously handling new data.

**Note that auto-delete does not apply to CSVs, including bulk uploads at high volumes.**

## **Enable auto-delete**

Follow these steps to set up auto-delete:

1.  Open a table.
    -   Note: Auto-delete only works with tables where the source is **webhooks**.
2.  Click the title of the table and select `Enable auto-delete`.
3.  Under **Auto-delete mode**, select one of the following options:
    -   **Disabled** — Rows will not be automatically deleted.
    -   **Delete when all actions finish** — Deletes rows once all action columns have finished running.
        -   Optionally, select a **Success column** from the dropdown. When set, a row will only become eligible for deletion after that specific column has run successfully. If no column is selected, rows are deleted as soon as all actions finish.
    -   **Delete based on conditional rules** — Deletes rows that match a set of custom filter conditions you define. Use this mode to trigger deletion based on more complex logic, such as time created or updated, values in a column, or column run status.
        -   Click `Add filter` to build your conditions. At least one filter rule is required to save this mode.
4.  Optionally, enter a value in the **Number of rows to keep** field. This sets how many of the most recent rows are retained in the table when auto-delete runs. Leave the field empty to use the default of 100 rows.
5.  Click `Save changes`.

**Warning:** Deleted rows are not recoverable.
