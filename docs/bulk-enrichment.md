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
    -   `Archive deleted rows` — When enabled, deleted rows are stored for up to 30 days and can be downloaded as a CSV. This toggle is off by default.
-   `Run starting point`: Choose how to handle rows already in the table when the run begins.
    -   **Continue where you left off** — Finishes enriching rows already in the table, then continues with the rest of the source.
    -   **Start from the beginning** — Clears rows already in the table and reruns everything from the source. Note: restarting will cost credits again for previously enriched rows.

## Queued rows and Errored rows

Bulk enrichment tables include two built-in tabs at the top of the view to help you track run progress:

-   **Queued rows** — rows that are waiting to be processed or are currently running.
-   **Errored rows** — rows where the action column tied to your deletion criterion did not complete successfully.

### Understanding Run Stopped

**Run Stopped** appears on a cell when the run was manually paused or stopped before that action had a chance to execute for that row. Because the action never ran, the row stays in the Queued rows or Errored rows tab (depending on your deletion criteria configuration) rather than completing normally.

-   **Single column** deletion criterion — rows with Run Stopped on the configured column appear in the **Errored rows** tab.
-   **Conditional rules** deletion criterion — rows with Run Stopped appear in the **Queued rows** tab.

This is why you may see rows in these tabs where some enrichment columns show successful results while one column shows **Run Stopped**: the upstream columns ran fine, but the final action (for example, **Update Audiences Record**) did not finish before the run was halted.

### How to re-run

Check both the **Queued rows** and **Errored rows** tabs for rows with **Run Stopped**. To retry:

1.  Right-click the column header showing **Run Stopped** → **Run column** → **Run [N] empty or out-of-date rows**.

For more options on re-running specific rows or cells, see [Run progress](run-progress.md).

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

-   **On** — any record that enters the segment after the initial run is automatically enriched in the background, typically within 15 minutes of joining the segment. This includes records that newly qualify because you updated your audience filters.
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