---
title: Apify integration overview
source_url: https://university.clay.com/docs/apify-integration-overview
description: Using Clay to run, monitor, and import data from Apify Actors.
last_synced: 2026-04-26T01:39:11.000Z
---

# Apify integration

Using Clay to run, monitor, and import data from Apify Actors.

[Apify](https://apify.com/) is a web scraping and automation platform that lets you run pre-built or custom Actors to collect and process web data. This integration lets you trigger Apify Actors directly from Clay, import results into your table, and use those results as inputs for further enrichment.

## Connecting to Apify

To connect your Apify account:

1.  In the home sidebar, click `Settings` → `Connections`.
2.  Click `Add connection` and search for `Apify`.
3.  Enter your Apify API token, which you can find in your [Apify account settings](https://console.apify.com/account/integrations).
4.  Click `Authenticate` to save the connection.

## Creating a table with Apify

1.  In a workbook, click `+ Add` at the bottom.
2.  Search for `Apify` and select from the results.
3.  In the modal, you will be asked to `Select Apify account`.
    -   If you haven't already connected your Apify account, click `+ Add account` and go through authentication.

### `Source` Import data from Apify

Import the output dataset from an Apify Actor run into Clay.

**Inputs:**

-   **Apify Actor:** Search for and select the Actor you want to run. Clay lists all Actors available in your Apify account.
-   **Actor input:** Configure the Actor's input parameters. These vary by Actor — refer to the Actor's documentation for the available fields and expected values.

**How the source works**

When you run the source, Clay triggers the selected Apify Actor, waits for the run to complete, and then imports all items from the Actor's output dataset into your Clay table. Each dataset item becomes one row.

**Note:** Running the Apify source consumes Apify compute units (your Apify account quota) in addition to any Clay credits. Very large Actor runs — for example, scraping hundreds of thousands of pages — may take longer than Clay's source timeout allows.

## Enriching data with Apify

While in a Clay table, click `Add enrichment` and search for `Apify`.

### `Action` Run Apify Actor

Trigger an Apify Actor run and retrieve the output.

**Inputs:**

-   **Apify Actor:** The Actor to run, selected from your Apify account.
-   **Actor input:** The input configuration for the Actor run. Map values from your Clay table columns using the `/` picker.

**How the action works**

The action triggers the selected Actor, waits for the run to finish, and returns the Actor's full output dataset as a JSON array in the enrichment result. You can then extract specific fields from the result using field-path selectors or a formula column.

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
