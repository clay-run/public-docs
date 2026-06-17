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

Login to Apify to select an actor. Select the scraper, and click `Create Task`. This will add it to your library of actors.

Switch from Manual to JSON and copy the body text. This will serve as your input data in Clay when you run the actor.

## Connecting to Apify in Clay

You can connect your Apify account to Clay in two ways:

### **Method 1: Connect Apify account within enrichment panel**

When running an Apify integration in Clay, you'll be prompted to **Add account**.

Add your API key and name it to create an account. You can find your API token on the [Integrations](https://console.apify.com/account#/integrations) page in the Apify Console.

### **Method 2: Connect Apify account through Clay settings**:

Navigate to **Settings** > **Connections** in your Clay dashboard.

Click on **Add Connection** and select Apify from the list.

Enter your Apify API key to establish the connection.

## Using the Apify integration

**Step 1: Choose Apify integration**

To connect Apify as a source: In a workbook, click `+ Add` at the bottom. Search for `Apify` and select from the results.  

If you are using Apify as an enrichment for an existing table, access the enrichment search bar by selecting **Add enrichment** in the top right corner. Type in "Apify" in the search bar and select **Run Apify Actor**.

**Step 2: Select Apify account**

Within the enrichment pane, select your Apify account, and add your account if you haven't already.

**Step 3: Select Apify actor and configure input data**

Select the Apify actor you want to run. Then In the **Input Data** section, you'll need to specify the data the actor will use. Enter the data body in JSON format.

When referencing column tokens (dynamic data from your Clay table), ensure the key is in quotes, but do not put quotes around the token itself. For example:

**Step 4: Configure run settings**

If you want to only run this enrichment under set circumstances, you are able to input formulas where the column runs only if the formula is true.

Autoupdate: By default, the auto-update automatically enriches new rows when they were added to the table. Make sure to toggle this step off if you do not want to auto-update, however, you might run into stale data problems.

Conditional run: If you want to only run this enrichment under set circumstances, you are able to input formulas where the column runs only if the formula is true. Learn more about conditional runs in [this Clay University lesson](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101).

Now you can run your Apify actor within your Clay table!

## Utilizing your Apify data

Click into the **Source Cell** for overlapping accounts to see all the data you pulled in from your Apify actor. From here, you can create new columns with the data or reference this data in an enrichment.

### Extracting specific values when output order varies

Apify actors each define their own output schemas. This means different rows can return data in a different order — one row might start with an Instagram URL, another with an email address, another with a phone number. Mapping by position produces inconsistent results in this case.

To reliably pull a specific type of value regardless of where it appears in the output, add an **Extract Values from Data** column (found under **Enrich Data**):

1. Add a new enrichment column and search for **Extract Values from Data**.
2. Set **Data** to your Apify output column.
3. Choose an **Extraction Type**:
   - **Email Addresses** — extracts all email addresses found in the data.
   - **Personal LinkedIn URLs** — extracts LinkedIn profile URLs.
   - **Domains** — extracts domain names.
   - **Custom (Advanced)** — enter a regex pattern to match any specific value type. For example, to extract Instagram profile URLs: `https?://(?:www\.)?instagram\.com/[^\s",]+`
4. The action returns a **Matches** list (all values found) and a **Joined Matches** string (comma-separated). Cells with no match show **No Matches Found**.

**Tip:** For output that varies too unpredictably for a regex pattern, use an [AI formula column](https://www.clay.com/university/lesson/how-to-use-ai-formulas) and prompt it to find the specific value — for example: *"Find the Instagram URL in {{Apify Results}}"*.

## Troubleshooting

### Incomplete imports

If the Import data from Apify source does not pull in your full dataset:

- Check whether rows were deleted from the table or auto-delete is enabled.
- Re-trigger the import to pull in missing data.
- Export the full CSV directly from Apify, import it into Clay, and compare the datasets to identify discrepancies.

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

1. Export the dataset as a CSV from Apify and upload it to Clay.
2. Use a Lookup from the imported table to the original table.
3. Filter rows to identify duplicates and their sources.

Note that duplicates often originate from Apify rather than Clay.

### "Actor run/dataset not found" errors

If Clay cannot pull a completed Apify dataset and shows an "Actor run/dataset not found" error:

- Verify the task or actor run ID for typos or accidental deletions.
- Ensure the Apify actor has completed runs with available data.
- Confirm the task is not private or restricted.

Scheduling the source to run regularly can help ensure new data is consistently imported.

### Preventing data overwrites

When re-running an action in Clay, existing results in the same column may be overwritten. To preserve previous results:

- Send the data to a new table immediately after it lands using **Write to other table** or **Send table data**.
- Each run is then saved separately, keeping prior results intact.

### Automating imports without overwrites

To automatically import data for multiple companies or URLs without overwriting previous results:

1. Use the native Apify integration to run the actor and retrieve results.
2. Schedule updates to run automatically.
3. Use **Write to other table** or **Send table data** to push results to a separate table so each run is saved independently.

### Rows running slowly or stuck in Queued — concurrency limit

Clay's native **Run Apify Actor** integration enforces a fixed limit of **4 concurrent requests**, regardless of your Apify plan. This limit applies to all workspaces and cannot be raised on a per-workspace basis — it is set to match the concurrency cap on Apify's lowest plan.

If rows are sitting in **Queued** status and you are on a higher-tier Apify plan, you can bypass this cap by calling Apify's API through an **HTTP API column** instead of the native integration. The HTTP API column does not apply this fixed limit, so Clay will dispatch requests at the rate your Apify plan supports. See the [HTTP API](http-api-integration-overview.md) guide for setup instructions.

### Actor runs timing out

The native **Run Apify Actor** integration has a **200-second execution limit**. If an actor takes longer than 200 seconds to complete, Clay will show **Timed out** in the result cell — even when the actor run itself succeeds in Apify.

This limit applies to all workspaces and cannot be raised on a per-workspace basis through the native integration.

**Workaround — two-step HTTP API approach:** For actors that regularly run longer than 200 seconds, switch to the [HTTP API integration](http-api-integration-overview.md) using an asynchronous two-step pattern:

1. **Column 1 — Start the run:** POST to Apify's `/v2/acts/{actorId}/runs` endpoint. This triggers the actor without waiting for it to finish and returns a `runId` immediately.
2. **Column 2 — Fetch the results:** Once the actor has had time to complete, GET `/v2/acts/{actorId}/runs/{runId}/dataset/items` to retrieve the results.

Because each HTTP API call completes in well under 200 seconds, your actor can take as long as it needs to finish between the two steps.
