---
title: Auto-delete in tables
description: Efficiently process and enrich large volumes of data using passthrough tables with compatible webhook, send table data, signal, and Audiences sources.
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
    -   Note: To fully bypass the 50,000 record source limit, the table source must be **webhooks**, **send table data**, a **signal source**, or an **Audiences source**. For all other source types, the source will still accumulate rows toward the 50,000 limit even with auto-delete enabled. A warning appears during setup if your table includes incompatible sources.
2.  Open the auto-delete settings using either access path:
    -   Click the **table title** and select **Enable auto-delete** from the dropdown, or
    -   Click the **auto-delete icon** (archive icon) in the bottom toolbar of the table.
3.  In the dialog that appears, check **This table uses a webhook, send table data, signal, or Audiences source.**, then click **Configure auto-delete**.
    -   If your table uses an incompatible source type, auto-delete will still delete rows, but the source record count continues accumulating toward the 50,000 limit.
4.  Under **Auto-delete mode**, select one of the following options:
    -   **Disabled** — Rows will not be automatically deleted.
    -   **Delete when all actions finish** — Deletes rows once all action columns have finished running.
        -   Optionally, select a **Success column** from the dropdown. When set, a row will only become eligible for deletion after that specific column has run successfully. If no column is selected, rows are deleted as soon as all actions finish.
    -   **Delete based on conditional rules** — Deletes rows that match a set of custom filter conditions you define. Use this mode to trigger deletion based on more complex logic, such as time created or updated, values in a column, or column run status.
        -   Click `Add filter` to build your conditions. At least one filter rule is required to save this mode.
5.  Optionally, enter a value in the **Number of rows to keep** field. This sets how many of the most recent rows are retained in the table when auto-delete runs. Leave the field empty to use the default of 100 rows.
6.  Click `Save changes`.

**Warning:** Deleted rows are not recoverable.

## Keeping space for incoming records

Auto-delete runs after records are written to the table, not before. When records arrive, Clay checks whether the table is below the 50,000-row limit and creates the records first — the auto-delete cleanup job then runs separately, typically about a minute later. This means that if records keep arriving faster than auto-delete can clear space, the table can temporarily reach the 50,000-row limit and new records will be rejected.

**Rejected records are not queued or retried.** If a record is turned away because the table is full, it is permanently lost — it will not be created once auto-delete runs and frees up space. For webhook sources, the sending system receives an error response (not a `200` status code), so you can detect the failure on the sending side and re-send if needed.

**Best practice:** Set **Number of rows to keep** to a value well below 50,000. For example, setting it to 40,000 creates a 10,000-row buffer — auto-delete continually trims the table back to 40,000, leaving room for new records to arrive before the limit is reached. Keeping this value too close to 50,000 increases the risk of the table bursting past the limit during a high-volume burst.

## Source compatibility

Not all source types support fully bypassing the 50,000 record import limit. Only the following source types clear the source record count when rows are deleted, allowing unlimited imports:

-   **Webhooks**
-   **Send table data**
-   **Signal sources** (e.g., web intent, job posts, news & fundraising, and other signal-based sources)
-   **Audiences**

All other source types — such as CRM integrations, Snowflake, and database connections — will continue accumulating toward the 50,000 limit even when auto-delete is enabled. Auto-delete will still delete rows from the table for those sources, but the underlying source record count is not cleared.

**Configuration warning:** When enabling auto-delete on a table that includes incompatible sources, Clay displays a warning: "This feature works for webhook, send table data, signal, and Audiences sources. All other source types will stop importing after 50,000 records, even with auto-delete enabled."

**Incompatible source banner:** If auto-delete is already enabled and your table has one or more incompatible sources, a warning banner appears on the table. The banner title reads "Auto-delete is on with a source that isn't compatible." when exactly one incompatible source is present, or "Auto-delete is on with sources that aren't compatible." when multiple incompatible sources are present. The banner highlights the source closest to the limit with a description like: "[source name] has processed 12,000 of 50,000 records maximum." A details view lists all incompatible sources with their counts in the compact format `12,000 / 50,000`. For tables with incompatible sources, you will need to manually delete rows to stay within the 50,000-record limit — auto-delete cannot prevent the source from hitting the cap for these source types.

**Continuous-streaming workflows:** Auto-delete allows a table to keep importing new records indefinitely only when the source continuously pushes incoming data — specifically, webhook, send table data, and signal sources. For scheduled CRM or database imports (such as Gong, Salesforce, HubSpot, or Snowflake queries configured to run on a recurring schedule), enabling auto-delete will delete processed rows from the table, but the source will still stop importing after 50,000 records are reached. To process records continuously — for example, enriching every new Gong call as it completes — use a **webhook source** in Clay and configure the external system to push records to Clay as they are created. For Gong specifically, you can do this with Gong's automation rules: create a webhook source in Clay, copy the webhook URL, then set up a Gong rule to send the call ID to that URL whenever a new call is processed.

## Archive deleted rows

**Note:** Archive deleted rows is in early access. Contact your Clay account team to have it enabled for your workspace.

When archive is enabled, the **Archive deleted rows** toggle appears in your auto-delete settings. Turning it on stores a copy of every auto-deleted row for up to 30 days after deletion. Archived rows can be downloaded as a CSV file from the History modal.

You can also select an **Indexed column** in the archive settings. Indexing a column lets you search for and retrieve specific deleted rows within the 30-day archive window.

To view deletion activity, open the **History** modal and select the **Auto-deleted rows** tab. The tab shows a daily and monthly breakdown of how many rows auto-delete has removed, so you can track throughput over time.
