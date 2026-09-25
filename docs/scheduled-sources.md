---
title: Scheduled sources
description: Automatically refresh data from sources on a set schedule.
last_synced: 2026-04-26T01:40:37.604Z
---

# Scheduled sources

Automatically refresh data from sources on a set schedule.

Schedule sources let you automatically refresh data from any source (like Find People, Find Jobs, Salesforce or HubSpot) on a recurring basis.

This keeps your data current without manual updates by pulling in new information at the frequency you set.

**Scheduled sources are not real-time.** Each run polls the connected system — records newly added to HubSpot, Salesforce, or another source appear in your Clay table only on the next scheduled run, not the moment they are created. The fastest available frequency is **hourly (Enterprise plans only)** or **daily (Launch and Growth plans)**. For updates that must appear in Clay immediately — for example, when a new HubSpot form submission should trigger enrichment within seconds — use a [webhook](webhook-integration-guide.md) instead.

## Scheduling source runs

**New sources:**

-   After adding a new source, a modal will appear to start scheduling runs.
-   Under `Run this source`, select `On a schedule`.
-   Choose the frequency and click `Update Source Schedule`.
    1.  Hour (Enterprise only)
    2.  Day
    3.  Week
    4.  Month
-   **Setting a custom start time or day of the week** (for example, every Sunday at 6:00 AM) is an Enterprise-only feature. Contact support if you don't see this option.
-   Toggle **Update existing rows**: When the source is re-run, any record **returned by that run** will have its existing row updated with the latest data. Records that are not returned by the source query — even if they were previously imported — will not be updated.

**For any existing sources:**

-   Click the source columns title.
-   Under `Sources`, select your source.
-   Under `Run this source`, select `On a schedule`.
-   Choose the frequency and click `Update Source Schedule`.
    1.  Hour (Enterprise only)
    2.  Day
    3.  Week
    4.  Month
-   **Setting a custom start time or day of the week** (for example, every Sunday at 6:00 AM) is an Enterprise-only feature. Contact support if you don't see this option.
-   Toggle **Update existing rows**: When the source is re-run, any record **returned by that run** will have its existing row updated with the latest data. Records that are not returned by the source query — even if they were previously imported — will not be updated.

**Scheduled source runs are additive.** Each run adds new records from the source to your table. Records that are no longer in the source — for example, contacts removed from a HubSpot list since the last run — remain in your Clay table and are not deleted. To remove rows that are no longer in the source, delete them manually or start fresh with a new table.

## Schedule time zones

The timezone shown next to a scheduled source's run time (for example, "11:57 GMT-3") reflects the system timezone of the computer used to set up that schedule — it is not a workspace-wide setting. Different sources in the same workspace can display different offsets if they were configured on computers with different timezone settings.

**There is currently no in-app control to select or change the timezone for a scheduled source.** The timezone label next to the "At:" field is a read-only display — clicking it does not open a selector. There is also no account- or workspace-level timezone preference that affects source schedules.

**If you need your source to run at a specific fixed time in a particular timezone (for example, 15:00 UTC):** temporarily change your computer's system clock to that timezone before entering the run time in the "At:" field. The schedule captures whichever timezone your OS is set to at the moment you save it. Once saved, the schedule runs at that captured offset on all future runs, regardless of any subsequent changes to your system clock.

**Note:** This timezone behavior applies to scheduled *sources* only (Salesforce, HubSpot, Find People, etc.). Scheduled enrichment column re-runs — configured in the table's Run Settings under **Re-run columns on a schedule** — support a **Custom** option that includes an explicit timezone picker (for example, every Sunday at 6:00 AM Eastern Time). See [Scheduled columns](scheduled-columns.md) for details.

## Triggering an immediate run

If you need to run a scheduled source right now — for example, after expanding a HubSpot list and not wanting to wait for the next scheduled run — you can trigger a one-time run without changing or canceling your existing schedule.

1.  Click the source column title in your table.
2.  In the source settings panel, scroll to the **Run settings** section.
3.  Click **Run now**.

The source runs immediately. Your schedule is unaffected — the next automatic run still fires at the time you configured.

## Usage limits

Scheduled sources are not available on the Free plan. For paid plans, the limit applies to the total number of scheduled sources across all tables.

-   Launch: 100 sources
-   Growth: 100 sources
-   Enterprise: 1,000 sources

If your workspace has reached its limit, you can remove schedules from sources you no longer need, or contact Clay support to request a higher limit.

## Troubleshooting

### What should I do when I see "workspace has reached the scheduled sources limit for your plan"?

This error appears when your workspace has reached the scheduled sources limit for its plan. It can occur when you try to schedule a source or when copying a table that contains scheduled sources.

To resolve it:

1.  **Remove the schedule from sources you no longer need.** Click the source column title in any table, then switch the source to run **Manually** (or delete the source entirely) to free up a slot. See [How can I find which tables have scheduled sources?](#how-can-i-find-which-tables-have-scheduled-sources) below for tips on identifying candidates.
2.  **Contact Clay support to request a higher limit.** Support can increase your workspace's scheduled sources limit on request.

### How can I find which tables have scheduled sources?

There is currently no dedicated view that lists all scheduled sources across a workspace. Two workarounds can help you identify candidates:

**Credit usage page:** Go to **Settings → Credit Usage** and filter by **Recurring**. This shows all tables with any recurring activity — scheduled sources, scheduled enrichment columns, or signals. Use this as a starting point to find tables to review.

**Connections page:** Go to **Settings → Connections** and filter by **Workbooks**. This shows all tables associated with a particular integration (for example, Salesforce). Tables named "Import records from [Provider]" are typically scheduled sources, though not all tables listed will have an active schedule.

Neither method produces a definitive list of only scheduled sources. If you need an exact count of your workspace's scheduled sources, contact Clay support.

### Can I filter the table to see only rows affected by a specific source run?

No. Clay does not provide a way to filter your table to show only the rows added or updated by a specific source run.

-   **Created At** reflects when a row was first inserted into the table — it only updates for net new rows. Existing rows that a source run updates in place do not get a new Created At timestamp, so filtering by today's date will show only newly added rows, not rows that were refreshed.
-   **Updated At** reflects the last time a row was written to. When a source run updates many rows at once, all of those rows receive the same Updated At timestamp — making it impossible to distinguish rows touched by a specific run from rows that were updated by other events on the same day.
-   The **Source history** panel (open the source column header → **View Run History**) shows a log of past runs with status, rows added, and date — but this is a run-level summary only. It does not let you filter the table to highlight the specific rows that run affected.

**Workaround — ensure enrichments re-run on all rows daily:** If your goal is to make sure every row in the table gets re-processed on each source run cycle (not just newly added rows), use **Re-run columns on a schedule**:

1.  Click the gear (`⚙`) icon in the bottom-right corner of your table to open **Table Settings**.
2.  Under **Run Settings**, toggle **Re-run columns on a schedule** on.
3.  Choose **Day** (or another frequency) and select which columns to re-run.

This forces the selected enrichment columns to re-run for every row on each cycle, regardless of whether the row was newly added or already existed. See [Scheduled columns](scheduled-columns.md) for full setup details, plan limits, and guidance on which column types to include or exclude from a scheduled re-run.

### Why isn't my Find Jobs table (or any source table) pulling new entries?

By default, sources — including Find Jobs — are configured to run **Manually**, meaning they perform a one-time import when first set up. New entries that match your filters are not pulled in automatically after that initial run.

To have your table automatically import new matching entries on a recurring basis, switch the source to run on a schedule:

1.  Click the source column title in your table.
2.  Under **Sources**, select your source.
3.  Under **Run this source**, select **On a schedule**.
4.  Choose a frequency (Daily, Weekly, or Monthly) and click **Update Source Schedule**.

Each subsequent run appends newly matched entries to your table without removing existing rows (see [Scheduled source runs are additive](#scheduling-source-runs) above).

**Note:** Scheduled sources are not available on the Free plan.
