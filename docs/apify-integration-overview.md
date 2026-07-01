---
title: Apify integration
description: Web scraping and automation platform providing data for AI and
  custom solutions, with troubleshooting for delayed imports, incomplete
  imports, duplicates, and data overwrites.
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

### No new data or delayed imports

If your Apify source table has not received new data, the source's refresh schedule is the most likely cause. By default, the source refreshes once daily. If the last scheduled run hasn't fired yet, new rows won't appear until the next refresh window.

To see when the next update is due or to trigger an import immediately:

1. Click the **database icon** in the Apify column header.
2. Select your source to open the source details sidebar.
3. Click **Run now** to pull in the latest data right away.

To change the refresh frequency, open the source settings from the same sidebar and update the schedule. Available options include daily, weekly, monthly, and quarterly; hourly is available on supported workspaces.

### Incomplete imports

If the Import data from Apify source does not pull in your full dataset:

- Check whether rows were deleted from the table or auto-delete is enabled.
- Re-trigger the import to pull in missing data.
- Export the full CSV directly from Apify, import it into Clay, and compare the datasets to identify discrepancies.

For large datasets, Clay fetches Apify dataset items in fixed batches of 50 rows per step, retrying automatically until all rows are retrieved. If rows are still missing after an import, trigger the import manually multiple times until the complete dataset appears.

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

### Actor column stuck in Queued — upstream column dependency

If your Apify actor column uses input data from another column (for example, a URL fetched by a preceding enrichment), it can sit in **Queued** status when that upstream column has not yet produced a value for that row.

**Fix:** Open the actor column's **Run Settings → Only run if** and add a run condition that gates execution on the required input being present. For example, if your actor reads from a column named "Website URL":

`/Website URL is not empty`

This ensures the actor only fires once the required data is available. If an existing run condition is already set and causing the issue, remove it and replace it with this one.

For full run condition syntax and examples, see [Conditional runs](conditional-runs.md). For other general steps when cells are stuck in Queued — including a hard refresh (`Ctrl+Shift+R` on Windows/Linux, `Cmd+Shift+R` on Mac) — see [Run progress](run-progress.md#troubleshooting-cells-stuck-in-queued-status).
