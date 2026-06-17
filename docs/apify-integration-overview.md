---
title: Apify integration
source_url: https://university.clay.com/docs/apify-integration-overview
description: Web scraping and automation platform providing data for AI and
  custom solutions, with troubleshooting for incomplete imports, duplicates,
  and data overwrites.
last_synced: 2026-04-26T01:39:40.957Z
---

# Apify integration

Web scraping and automation platform providing data for AI and custom solutions.

## Apify Integration Overview

With Clay's Apify integration, you can quickly retrieve data from Apify actor runs or launch actors directly in Clay to get results on demand.

## Setting up in Apify

To set up Apify:

1.  Log in to your Apify account and [retrieve an API token](https://console.apify.com/account/integrations). Name it something clear for future reference.
2.  In Clay, navigate to Settings → Connections.
3.  Click Add connection, find the Apify integration, and paste the token.

## Enriching data with Apify

1.  While in a Clay table, click `Add enrichment` and search for `Apify`.
2.  Under `Integrations`, select one of the Apify options.
3.  In the modal, you will be asked to `Select Apify account`.
    -   If you haven't already connected your Apify account, click `+ Add account` and go through authentication.

### `Source` Import data from Apify

Import data from an Apify actor.

-   **Actor ID**: The ID of the actor to run. You can find the actor ID in the Apify console.
-   **Actor Input**: The input data for the actor. This is a JSON object that specifies the data to be processed.

### `Action` Get actor results

Get the results of an Apify actor from a previously started run.

-   **Actor ID**: The ID of the actor to run. You can find the actor ID in the Apify console.
-   **Actor Input**: The input data for the actor. This is a JSON object that specifies the data to be processed.
-   **Run ID**: The run ID of the actor run to retrieve results from.

### `Action` Run Actor

Run an Apify actor.

-   **Actor ID**: The ID of the actor to run. You can find the actor ID in the Apify console.
-   **Actor Input**: The input data for the actor. This is a JSON object that specifies the data to be processed.

## FAQs

### Why is the Apify source not pulling in all my data?

If the Import data from Apify source does not pull in your full dataset:

-   Check your Actor input configuration — missing or incorrect parameters can cause the Actor to return partial results.
-   Verify the Actor run completed successfully in the Apify console before re-running the source in Clay.
-   Re-trigger the import to pull in missing data.

If re-triggering the import shows 0 new rows added, the source may have reached the 50,000-record limit — see [Scheduled Apify source stopped adding new rows](#scheduled-apify-source-stopped-adding-new-rows-after-hitting-the-50000-record-limit) below.

For large datasets, Clay fetches Apify dataset items in fixed batches of 50 rows per step, retrying automatically until all rows are retrieved. If rows are still missing after an import, trigger the import manually multiple times until the complete dataset appears.

### Scheduled Apify source stopped adding new rows after hitting the 50,000-record limit

If your Apify source is set to run on a schedule but has stopped adding new rows — even though Apify shows successful actor runs with data — the most likely cause is that the source has accumulated 50,000 records and is now silently discarding all incoming data.

**Important:** This is the *source record count*, not the number of rows currently visible in your table. Clay tracks every record a source has ever imported, including rows you have since deleted from the table. Deleting rows does **not** reset this counter — a table can show far fewer than 50,000 visible rows while the source has already reached the 50,000-record limit.

The schedule itself is not broken — it continues to fire normally. But at the point of inserting records, Clay silently discards all incoming data without displaying an error or sending a notification.

**To resolve this:**

1. **Create a new source definition.** Delete the current Apify source and add it again with the same settings. A new source starts at a fresh 0/50,000 record count. Alternatively, create a new table and add the Apify source there.
2. **Enable auto-dedupe before re-adding the source.** If your new source will import records already present in the table, enable [auto-dedupe](table-management-settings.md) on a unique identifier column (such as a profile URL or company domain) to automatically remove duplicate rows.

For more on the 50,000-record source limit and workarounds for large ongoing imports, see [What are the row limits for Clay tables and sources?](sources.md#what-are-the-row-limits-for-clay-tables-and-sources).

### Duplicate data

To resolve duplicate data:

-   Ensure **Auto-dedupe** is enabled on a unique identifier column (such as a profile URL) before running or re-running the source. Auto-dedupe prevents duplicate rows from being added when the same Actor is run multiple times.
-   If duplicates already exist, use Clay's built-in deduplication tools to identify and merge them.

### Data is getting overwritten

If data is getting overwritten when running the source multiple times:

-   Enable Auto-dedupe before running the source (if you have already run the source and need to deduplicate, you can still enable this setting).
-   Ensure that the data that you're running on doesn't already exist in the destination table.
