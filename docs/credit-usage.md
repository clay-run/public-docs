---
title: Credit usage
description: Track credit consumption across your workspace.
last_synced: 2026-05-04T00:00:00.000Z
upstream_hash: 49adc53e477510baa3bbdef7bf19e66afe61d2d6471b8803966d822f686ba5a4
---

# Credit usage

Track credit consumption across your workspace.

Track, analyze, and optimize your credit consumption by breaking down usage across workbooks, tables, and integrations.

## Credit usage dashboard

To check the credit usage in your workspace:

1.  Click your account name in the corner.
2.  Go to `Settings` and then `Usage` in the sidebar.
3.  Within `Workspace`, you can view folders, workbooks, and tables sorted by their usage.

**Tip:** If your workspace is approaching or has reached its monthly credit limit, Clay displays an orange banner at the top of every page. Click **See usage** in that banner to go directly to the credit usage dashboard.

**Tip:** The credit indicator in the top navigation bar shows your **remaining** balance, labeled **"X credits available"** — this is how many credits you have left to spend this period, not how many you have already consumed. To see your credit consumption (how much you've spent), use the credit usage dashboard at `Settings → Usage`.

Sort the content by `Name` (alphabetically) or by number of `Credits used` by clicking the column titles. You can `Export` this content as a CSV.

### Filter and sort credit usage

The columns in this view display:

-   `Name:` The folder, workbook, or table. Click the dropdown next to a folder or workbook to see the contents.
-   `Usage:` Marked as `Recurring` when it contains recurring credit usage (e.g., scheduled runs or signals).
-   `Owner:` The workbook's creator or assigned owner — not necessarily who triggered the credit spend within it.
-   `Credits used:` The amount of credits used for this period. On the top-level **Workspace** row, this total includes credits from tables that have since been deleted. Hover over the ⓘ icon on the Workspace row to see how many credits came from deleted tables.

Filter any of the content on this page by:

1.  **When the credits were used** — use the `When` dropdown to select a preset period (`This week`, `Last week`, `This month`, or `Last month`) or choose `Custom range` to enter a specific start and end date. This lets you scope the dashboard to any window — for example, to see how many credits you used in a single day or between two specific dates.
2.  Owner of the workbook (its creator, not who ran the enrichments).
3.  Specific integrations being used.
4.  **Recurring runs only:** Toggle `Recurring` to show only credits from recurring or scheduled runs. By default (toggle off), the dashboard shows all credit consumption — both one-time manual runs and recurring automated runs. When this filter is on, only workbooks and tables with recurring usage are shown in the expanded list — but folder and workbook `Credits used` totals always reflect the complete spend for all their contents, including non-recurring workbooks. If a folder's total appears higher than the sum of the workbooks visible when you expand it, the difference comes from non-recurring workbooks hidden by the filter. Toggle the filter off to see all workbooks and their individual credits.

**Note:** The Workbooks tab does not show per-user credit attribution — it groups spend by workbook or table, not by which team member ran the enrichments. If you need per-user credit tracking, see the **MCP** and **API** tabs, which attribute spend to individual users for those access methods.

### Understanding table-specific credit usage

For deeper insights into credit spend within a specific table, you can access the table credit usage dashboard. This gives you realtime data on when and how credits were spent within that table.

**Note:** Historical data for the table credit dashboard begins on November 5th, 2025. You'll see a warning about incomplete data if your selected time range begins before this date.

**How to access the table dashboard:**

_From a table:_

-   Click the `Credit usage` button within the Credits popover and select `Table credit usage`.
-   Click the `History` button in the lower right corner of your table and select `Usage history`.

_From the workspace credit dashboard:_

-   Click the chart button next to any table's name to open its table-level dashboard.

**Dashboard views:**

The table credit dashboard offers three ways to analyze your credit spend:

`Time view:` See a time series graph of your table's credit spend over time. You can:

-   Choose your time range
-   Aggregate by different time units (day, week, month)
-   Break down each bar by action type to see what consumed credits

`Column view:` See your spend broken down by each column in your table, helping you identify which enrichments are using the most credits.

`Run view:` See spend events grouped by run, where a run could be:

-   A manual action (clicking the `Run` button on a column)
-   An automated action (scheduled source import or auto-update)

All views allow you to download the data as a CSV for further analysis.

**Note:** Historical data for the table credit dashboard begins on November 5th, 2025. You'll see a warning about incomplete data if your selected time range begins before this date.

### Checking credit cost for a specific action on a row

The workspace and table dashboards break down spend by workbook, table, column, or run — but not by individual row. To see what a specific enrichment charged on a particular row, click on that **action cell** directly. The cell details panel shows a **Charged** line with the data credits consumed by that enrichment for that row.

This is useful for spot-checking costs before scaling a workflow: run a small batch of rows, click into individual action cells to see per-enrichment charges, then use those figures to estimate total credit cost at higher volumes.

## **Credit usage breakdown**

The credit usage dashboard is organized into tabs, each covering a different slice of your workspace spend. Use the `When` dropdown and `Apply filters` to scope each tab to a specific time period.

-   **Workbooks** — shows credit spend broken down by folder, workbook, and table. Click the dropdown next to any folder or workbook to drill into its contents. Sort by `Name` or `Credits used`. Click `Export` to download a CSV for offline analysis.
-   **Integrations** — shows credit spend grouped by integration across your entire workspace. Expand any integration row to see a breakdown by individual API key — useful when you have both Clay-managed and personal (BYOK) keys connected, or multiple keys for the same provider. Sort by `Name` or `Credits used`. Click `Export` to download a CSV.
-   **Signals** — shows credit spend broken down by individual signal. A totals row (`All Signals`) appears at the top, followed by a per-signal breakdown of `Credits used` and `Actions used`.
-   **MCP** — shows programmatic spend from team members who access Clay through ChatGPT or Claude, broken down by user. Spend that can't be attributed to a specific user appears as `Unattributed`. For per-user credit limits and live usage tracking, see `Settings → MCP users`.
-   **API** — shows programmatic spend generated through Clay's API and Exportly, broken down by user. Like MCP, unattributable spend appears as `Unattributed`.
-   **Budgets** — shows credit spend broken down by budget. Visible only on workspaces with Credit Budgets enabled (currently in open beta for Enterprise customers). See [Credit Budgets](/docs/credit-spend-limits-faq#credit-budgets-open-beta) for details.

**Note:** The `Credits used` total on the **Workbooks** tab reflects only workbook and table activity. Credits consumed by Signals, MCP, or API access appear on those respective tabs and are not included in the Workbooks total. To see your complete workspace credit spend for a given period, review the totals across all relevant tabs.

## Credit estimates before running

Clay provides transparent cost estimates before you run enrichments or actions in your tables. This helps you understand and manage your credit usage.

### Run cost breakdown

When you run a column that has dependent columns (downstream enrichments that will automatically trigger), you'll see:

-   Total estimated credits for the run.
-   Breakdown by column showing which columns will run and their individual costs.
-   Number of rows that will be affected.

This estimate appears for any column run that would trigger dependent enrichment columns, including runs initiated by:

-   Manual column runs
-   Changes to data sources
-   Adding new rows

**Variable AI pricing estimates:** A `~` prefix on a cost in the estimate (e.g., `~65/row`) means that figure is approximate. This applies to AI columns using variable pricing — actual costs per row may be higher or lower depending on the complexity of each prompt and the data processed. To calibrate expected spend before running a large table, run the column on a small batch of 10–50 rows first, then check the per-row cost in the table. See [How AI is priced](/docs/ai-pricing) for full details on variable vs. fixed AI pricing.

### Expensive run warnings

Clay shows a warning when you're about to initiate a run that will use a significant portion of your workspace's monthly credit allotment. Specifically:

-   Runs that cost more than 10% of your monthly credit allotment.
-   With a minimum threshold of 500 credits.
-   Runs over 50,000 credits will always trigger this warning.

This helps prevent accidental large credit expenditures.

### Import warnings

When you import data to existing tables (via Copy Paste from URLs, adding a source, or CSV upload), you'll see a confirmation modal if the import would trigger downstream actions. This modal:

-   Warns you about potential credit usage from auto-running enrichments
-   Shows estimated credit impact
-   Gives you the option to toggle auto-run off for the table before importing

This prevents unexpected credit usage when you add new data to tables with existing enrichment workflows.

## Troubleshooting unexpected credit usage

### Enrichments ran on all rows when setting up a new table

The import warning and the first-10-rows auto-run limit both protect you when **adding a source to an existing table** — but neither applies when you create a **brand-new table** with a source and enrichment columns for the first time.

-   **No import warning**: Clay shows the confirmation modal only when a source is added to a table that already has enrichment columns. A new table has no action columns at the moment the source first runs, so no credit-spend warning appears.
-   **Enrichments fire on all imported rows**: The first-10-rows auto-run limit only applies when importing into an existing table. For a new table, enrichments with auto-run enabled queue on every row the source imports — not just the first 10.

To safely test a new table before committing credits at scale:

1.  Turn table-level auto-run **off** before running your source for the first time (click `⛭` → toggle **Auto-run** off).
2.  Import your source — rows load into the table without triggering any enrichments.
3.  Select 5–10 rows, right-click, and choose **Run rows** to manually test your enrichments on a small batch.
4.  Click individual action cells to see the **Charged** value and confirm the per-row cost.
5.  Once you're satisfied, turn auto-run back **on** and choose **Update cells** to process the remaining rows.

See [Ways to save Clay credits](clay-credit-conservation.md) for the full recommended testing workflow.

### Credits consumed while auto-run is off

If table-level auto-run is disabled but credits are still being consumed, the most likely causes are manual or team-triggered actions:

-   **Manual column runs** — any Editor on the workspace can right-click a column header and choose **Run column**, which bypasses the auto-run toggle and immediately dispatches enrichments.
-   **Scheduled columns** — a column may have a recurring schedule that runs independently of the table's auto-run setting. Open **Run Settings → Re-run columns on a schedule** to review which columns are scheduled and disable any you no longer need. See [Ways to save Clay credits](clay-credit-conservation.md) for guidance on auditing scheduled runs.
-   **Hidden columns with auto-run enabled** — columns that are hidden from view still run if their individual auto-run toggle is on. Open the columns panel to check for hidden columns and disable auto-run for any you don't need actively running. See [Table columns overview](table-columns-overview.md) for details.

To identify what triggered a specific run, use the **Run view** in the [table credit usage dashboard](#understanding-table-specific-credit-usage). Each entry shows whether the run was manual, automated, or scheduled, along with a timestamp.

### Credits consumed after clicking Stop or Cancel

Clicking **Stop** on a running table or canceling a column run does not immediately halt all enrichments. Clay cancels cells that are still queued (not yet dispatched), but any requests already sent to an external data provider will run to completion and consume credits. You may see a brief delay before the table fully halts while these in-progress calls finish.

To avoid unexpected spend before it starts, disable [auto-run](table-management-settings.md) before importing large batches of rows. See [Stopping a run](run-progress.md) for full details on stop and cancel behavior.

### Credits spiked after editing a formula or upstream column

When you edit a formula in a column that other enrichments reference, Clay marks all downstream cells as stale. With auto-run in its default **run all cells** mode, this queues a re-run for every stale cell across all rows — which can trigger every dependent enrichment column at once and produce a large, unexpected credit charge.

To avoid this, enable **Keep existing results** before making formula or configuration changes:

1.  Click `⛭` in the top toolbar to open Run Settings.
2.  Check **Keep existing results**.

With **Keep existing results** on, auto-run only fires on cells that are empty or errored — cells that already have a result are skipped, even when their upstream formula changes. This lets you update formulas without re-running (and re-charging) your entire table.

Alternatively, turn auto-run **off** entirely before editing (`⛭` → toggle **Auto-run** off), make your changes, then manually run only the specific rows or columns you need.

See [Table management settings](table-management-settings.md) for full details on **Keep existing results** and how the auto-run mode affects which cells run.

### Requesting a goodwill credit refund

If credits were accidentally consumed — for example, from a misconfigured scheduled run or an unintended large batch — you can contact [Clay support](https://app.clay.com) to request a one-time goodwill credit refund. When submitting a request, include:

-   Your workspace name
-   The table where the credits were consumed
-   The number of credits used

The support team will review your request and, if eligible, restore the credits to your account balance. Goodwill refunds are a one-time exception and are not guaranteed for repeat requests. For credits consumed due to a scheduled table run or integration issue, a partial refund may be considered depending on the circumstances.

**Learn more:** For related information, check out our [credit limit FAQs doc](http://university.clay.com/docs/credit-spend-limits-faq).
