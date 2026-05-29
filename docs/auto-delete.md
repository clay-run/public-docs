---
title: Auto-delete in tables
source_url: https://university.clay.com/docs/auto-delete
description: Efficiently process and enrich large volumes of data using passthrough tables with compatible webhook, send table data, and signal sources.
last_synced: 2026-04-26T01:39:41.622Z
---

# Auto-delete in tables

Efficiently process and enrich large volumes of data.

**Note:** This is a feature available to users on the Enterprise Plan.

Auto-delete is a powerful feature designed to help you process and enrich large volumes of data efficiently. It allows you to bypass the standard row limit by automatically processing incoming data, enriching it, and then forwarding it to a designated destination before deleting the original entries from the table. This ensures your tables remain manageable while continuously handling new data.

**Tip:** You can receive advance warning before your table reaches the row limit by enabling the **Row count limit** alert in [Table alerts](table-alerts.md). The default threshold is 45,000 rows, and notifications can be delivered via email or Slack. Table alerts are opt-in and configured per table — no notification is sent automatically when a table hits the 50,000-row limit.

**Note that auto-delete does not apply to CSVs, including bulk uploads at high volumes.**

## **Enable auto-delete**

Follow these steps to set up auto-delete:

1.  Open a table.
    -   Note: To fully bypass the 50,000 record source limit, the table source must be **webhooks**, **send table data**, or a **signal source**. For all other source types, the source will still accumulate rows toward the 50,000 limit even with auto-delete enabled. A warning appears during setup if your table includes incompatible sources.
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

## Source compatibility

Not all source types support fully bypassing the 50,000 record import limit. Only the following source types clear the source record count when rows are deleted, allowing unlimited imports:

-   **Webhooks**
-   **Send table data**
-   **Signal sources** (e.g., web intent, job posts, news & fundraising, and other signal-based sources)

All other source types — such as CRM integrations, Snowflake, and database connections — will continue accumulating toward the 50,000 limit even when auto-delete is enabled. Auto-delete will still delete rows from the table for those sources, but the underlying source record count is not cleared.

**Configuration warning:** When enabling auto-delete on a table that includes incompatible sources, Clay displays a warning: "This feature only works for webhook, send table data, and signal sources. All other source types will stop importing after 50,000 records, even with auto-delete enabled."

**Incompatible source banner:** If auto-delete is already enabled and your table has one or more incompatible sources, a warning banner appears on the table. The banner title reads "Auto-delete is on with a source that isn't compatible." when exactly one incompatible source is present, or "Auto-delete is on with sources that aren't compatible." when multiple incompatible sources are present. The banner highlights the source closest to the limit with a description like: "[source name] has processed 12,000 of 50,000 records maximum." A details view lists all incompatible sources with their counts in the compact format `12,000 / 50,000`. For tables with incompatible sources, you will need to manually delete rows to stay within the 50,000-record limit — auto-delete cannot prevent the source from hitting the cap for these source types.
