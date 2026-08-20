---
title: Bulk enrichment
description: Enrich millions of rows quickly, securely, and at scale. No row
  limits, no slowdown.
last_synced: 2026-04-27T18:09:27.586Z
---

# Bulk enrichment

Enrich millions of rows quickly, securely, and at scale. No row limits, no slowdown.

# Bulk enrichment

**Bulk enrichment** makes it easy to process massive datasets—no row limits, no slowdown. Enrich millions of rows quickly, securely, and at scale.

You'll get the full power of Clay's enrichment engine without storing data inside Clay. Results are sent directly to your external destinations, like Salesforce, Snowflake, or Google Sheets, keeping your systems continuously enriched and in sync.

Once your data is successfully exported, enriched rows are automatically deleted to keep your workspace clean and efficient.

## Setting up a bulk enrichment

### Import from CSV

1.  On the homepage, click `New` → `Bulk enrichment`.
2.  Select `Source type` → `Import from CSV`.
3.  Select `Delimiter`.
    -   A delimiter is the character that separates values in your CSV file (e.g., comma, semicolon, or tab).
4.  Click `Save` and start adding [enrichments](https://www.clay.com/university/guide/enrichments) normally.

### Import from CRM (Salesforce)

1.  On the homepage, click `New` → `Bulk enrichment`.
2.  Select `Source type` → `Import from CRM`.
3.  Next, `Select Salesforce account`.
    -   Click `Add account` if you haven't already authenticated your account.
4.  Select inputs from `Salesforce object` and `List view`.
5.  Click `Save` and start adding [enrichments](https://www.clay.com/university/guide/enrichments) normally.

### Using a bulk enrichment

In the bulk enrichment settings, you can adjust several options:

-   `Test data`: Add rows to test your enrichments before running the full source.
-   `Export data`: Set up your export destination.
    -   This could be Salesforce, Google Sheets, Snowflake, etc.
-   `Deletion criteria`: Choose when a row is considered complete and automatically deleted. This setting is required — leaving it unconfigured shows an **Incomplete configuration** error that prevents the run from starting.
    -   **Single column** — Deletes the row once a selected column has run, or if any conditional rules determine the column doesn't need to run. After selecting this option, use the **Select field** dropdown to pick the specific column that signals a row is complete and ready to be deleted or archived. Typically this is your export action column — for example, the column that adds a row to Google Sheets.
    -   **Conditional rules** — Combine multiple rules or columns to trigger deletion.
    -   `Archive deleted rows` — When enabled, deleted rows are stored for up to 30 days and can be exported as a CSV from the Archive view. Archived rows are read-only — they cannot be moved back into the live table for re-processing. This toggle is off by default.
-   `Run starting point`: Choose how to handle rows already in the table when the run begins.
    -   **Continue where you left off** — Finishes enriching rows already in the table, then continues with the rest of the source.
    -   **Start from the beginning** — Clears rows already in the table and reruns everything from the source. Note: restarting will cost credits again for previously enriched rows.

## Queued rows and Errored rows

Bulk enrichment tables include two built-in tabs at the top of the view to help you track run progress:

-   **Queued rows** — rows that are waiting to be processed or are currently running.
-   **Errored rows** — rows where the action column tied to your deletion criterion did not complete successfully.

Unlike standard Clay tables, the bulk enrich view does not include a custom filter builder — the **Queued rows** and **Errored rows** tabs are the only built-in views. Completed rows are automatically deleted based on your deletion criteria and are no longer visible in the bulk enrich view.

To inspect specific records before or after processing, here are some alternatives:

-   **Filter at the source** — Narrow your data before it enters bulk enrichment. For example, use a filtered list view in Salesforce, or pre-filter your CSV before importing.
-   **Use test data** — Use the **Test data** option in your bulk enrichment settings to add a small subset of rows and verify output before running the full source.
-   **Review results at the destination** — Once enriched rows are exported to your destination (Salesforce, Google Sheets, Snowflake, etc.), filter and review them there.

### Understanding Run Stopped

**Run Stopped** appears on a cell when the run was manually paused or stopped before that action had a chance to execute for that row. Because the action never ran, the row stays in the Queued rows or Errored rows tab (depending on your deletion criteria configuration) rather than completing normally.

-   **Single column** deletion criterion — rows with Run Stopped on the configured column appear in the **Errored rows** tab.
-   **Conditional rules** deletion criterion — rows with Run Stopped appear in the **Queued rows** tab.

This is why you may see rows in these tabs where some enrichment columns show successful results while one column shows **Run Stopped**: the upstream columns ran fine, but the final action (for example, **Update Audiences Record**) did not finish before the run was halted.

### How to re-run

Check both the **Queued rows** and **Errored rows** tabs for rows with **Run Stopped**. To retry:

1.  Right-click the column header showing **Run Stopped** → **Run column** → **Run [N] empty or out-of-date rows**.

For more options on re-running specific rows or cells, see [Run progress](run-progress.md).

### Understanding count differences between Clay and your destination

When a bulk enrichment contains multiple enrichment steps, the record count shown in Clay and the count in your downstream destination (Snowflake, Salesforce, Google Sheets, etc.) will often differ while a run is in progress. **This is expected behavior, not a bug.**

Each enrichment step processes independently with its own queue and latency. Clay's processed count increments when a row exits the bulk enrichment table — but the final write to your destination only completes after all upstream enrichment steps for that row have finished. As the work drains through the chain, the two counts catch up to each other.

For example, if your bulk enrichment runs several function-based enrichment steps before a Snowflake export, you may see Clay reporting 46,000 records processed while Snowflake shows only 14,000 rows — because thousands of rows are still working through the intermediate steps.

**Why destination counts keep climbing after you pause a run**

Pausing a bulk enrichment stops new rows from entering the processing queue. However, rows that were already dispatched to enrichment steps continue running to completion. This means your downstream destination (Snowflake, Salesforce, etc.) may keep receiving new writes for some time after the table is paused — the in-flight work is still finishing. Once those rows complete, the destination count stabilizes.

**How to reconcile counts**

To understand where rows are in the pipeline:

1.  Start from your final write action (for example, your Snowflake or Salesforce export column) and check its progress bar.
2.  Work backwards through the enrichment chain, checking the progress of each step.

Each enrichment column shows a progress bar you can hover over to see how many rows have completed, are queued, or have errored at that step. Comparing the counts across steps shows exactly where rows are still in flight.

## Run Setup settings (Audiences)

When a bulk enrichment is attached to an [Audiences](https://university.clay.com/docs/audiences) segment (available on Growth and Enterprise plans), clicking the enrichment card opens a **Run Setup** panel with additional settings for ongoing enrichment behavior.

### Field mapping

The **Field mapping** setting controls whether enriched data is written back to your Audiences records after each row runs.

-   **On (default)** — enriched data is sent to Audiences. Click **Set up** to configure which columns map to which Audience fields. At least one column must be mapped before you can start the run — clicking **Start Run** without completing this step shows an inline error: *"Map at least one column, or turn off field mapping."*
-   **Off** — the Send to Audiences step is skipped for every row. No data is written back to Audiences, and each row shows **✅ Skipped** in the results column.

To turn field mapping off, click **Set up** in the Run Setup panel, then toggle **Field mapping** off at the top of the configuration panel.

Turn field mapping off when you want to run enrichments and route results somewhere else — for example, writing directly to Salesforce via an action column — without also writing the data back to Audiences.

### Auto-enrich new records

The **Auto-enrich new records** toggle determines whether records that newly qualify for the segment are enriched automatically after the initial run.

-   **On** — any record that enters the segment after the initial run is automatically enriched in the background, within 20 minutes of joining the segment. This includes records that newly qualify because you updated your audience filters.
-   **Off** — only records present at the time of the initial run are enriched. Records that join the segment later are not enriched automatically.

**To change this setting while a run is active:** click **Pause** first. The toggle is locked while the enrichment is running and can only be changed when the enrichment is paused or not yet started.

### Recurring enrichments

**Recurring enrichments** re-enrich all records in the segment on a schedule, keeping enriched fields up to date over time (for example, refreshing job titles or company data monthly).

To set a schedule, click **Recurring enrichments** in the Run Setup panel and select your desired frequency.

### What happens when you click Start Run

When you click **Start Run** on an Audiences bulk enrichment, Clay recalculates your **live segment at that moment** using your current filters — not the member list baked in when the bulk enrichment was first created. The live segment is the source of truth for the run.

**The preview rows displayed in setup mode reflect your segment membership at the time the bulk enrichment was created** — they do not automatically refresh as you edit your segment filters. This is a known limitation the team is actively working to address in a future update.

Here's what happens to setup-mode rows when you click **Start Run**:

-   **Records that no longer match your current segment** — these are automatically deleted from the bulk enrichment. They will not be enriched, and you will not be charged credits for them.
-   **Records that still match your current segment** — these are re-enriched from scratch. Credits are spent again for these rows.

This means if you updated your audience segment filters after creating a bulk enrichment, you do not need to manually remove records that no longer match before running — clicking **Start Run** handles cleanup automatically.

### Resuming after changing segment filters

If you pause a bulk enrichment and update your audience segment before resuming, the resume option you choose determines which records are picked up next.

**Continue where you left off**

Records already in the queue finish processing first. What happens to newly-qualifying records depends on how you changed your segment:

-   If you **added a new segment** to the bulk enrichment while it was paused, members of the newly-added segment are enqueued automatically when you resume.
-   If you **edited the filter conditions on an existing connected segment** (same segment, narrowed or changed the filters), records that newly match the updated filters are **not** automatically enqueued on resume. Clay tracks which segment IDs were connected at the time the run was paused — it does not re-evaluate membership changes from in-place filter edits when resuming.

If you edited an existing segment's filters and want those newly-qualifying records to be enriched, use **Run from the beginning** instead. Alternatively, if **Auto-enrich new records** is enabled, newly-qualifying records will be picked up automatically in the background within 20 minutes of joining the segment.

**Run from the beginning**

All rows currently in the bulk enrich table are cleared, and the enrichment restarts fresh using your current segment configuration — including any filter changes you made to existing connected segments. Previously archived rows from the completed portion of the run are not affected — they remain in the archive. Note: restarting costs credits again for the newly seeded rows.

**Which option to use:**

-   Choose **Continue where you left off** if you want to finish processing records already in the queue. Note that if you edited an existing segment's filter conditions (rather than adding a new segment), those newly-qualifying records will not be pulled in automatically on resume.
-   Choose **Run from the beginning** if you edited the filter conditions on an existing connected segment and want the enrichment to start fresh using your updated filters. This clears the current queue and seeds the run from your current segment configuration.
