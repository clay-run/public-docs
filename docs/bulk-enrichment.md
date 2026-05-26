---
title: Bulk enrichment
source_url: https://university.clay.com/docs/bulk-enrichment
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
-   `Deletion criteria`: Single column or conditional rules.
    -   You can also `Archive deleted rows` for up to 30 days, meaning they will remain indexed and searchable.
-   `Run starting point`: Decide whether to clear rows already in the test table and rerun them.

## Run Setup settings (Audiences)

When a bulk enrichment is attached to an [Audiences](https://university.clay.com/docs/audiences) segment (available in beta for Enterprise customers), clicking the enrichment card opens a **Run Setup** panel with additional settings for ongoing enrichment behavior.

### Auto-enrich new records

The **Auto-enrich new records** toggle determines whether records that newly qualify for the segment are enriched automatically after the initial run.

-   **On** — any record that enters the segment after the initial run is automatically enriched in the background, typically within 15 minutes of joining the segment. This includes records that newly qualify because you updated your audience filters.
-   **Off** — only records present at the time of the initial run are enriched. Records that join the segment later are not enriched automatically.

**To change this setting while a run is active:** click **Pause** first. The toggle is locked while the enrichment is running and can only be changed when the enrichment is paused or not yet started.

### Recurring enrichments

**Recurring enrichments** re-enrich all records in the segment on a schedule, keeping enriched fields up to date over time (for example, refreshing job titles or company data monthly).

To set a schedule, click **Recurring enrichments** in the Run Setup panel and select your desired frequency.
