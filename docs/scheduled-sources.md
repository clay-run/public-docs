---
title: Scheduled sources
description: Automatically refresh data from sources on a set schedule.
last_synced: 2026-04-26T01:40:37.604Z
---

# Scheduled sources

Automatically refresh data from sources on a set schedule.

Schedule sources let you automatically refresh data from any source (like Find People, Find Jobs, Salesforce or HubSpot) on a recurring basis.

This keeps your data current without manual updates by pulling in new information at the frequency you set.

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

## Troubleshooting

### Why isn't my Find Jobs table (or any source table) pulling new entries?

By default, sources — including Find Jobs — are configured to run **Manually**, meaning they perform a one-time import when first set up. New entries that match your filters are not pulled in automatically after that initial run.

To have your table automatically import new matching entries on a recurring basis, switch the source to run on a schedule:

1.  Click the source column title in your table.
2.  Under **Sources**, select your source.
3.  Under **Run this source**, select **On a schedule**.
4.  Choose a frequency (Daily, Weekly, or Monthly) and click **Update Source Schedule**.

Each subsequent run appends newly matched entries to your table without removing existing rows (see [Scheduled source runs are additive](#scheduling-source-runs) above).

**Note:** Scheduled sources are not available on the Free plan.
