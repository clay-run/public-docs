---
title: Credit usage
source_url: https://university.clay.com/docs/credit-usage
description: Track credit consumption across your workspace.
last_synced: 2026-05-11T17:47:40.000Z
---

# Credit usage

Track credit consumption across your workspace.

Track, analyze, and optimize your credit consumption by breaking down usage across workbooks, tables, and integrations.

## Credit usage dashboard

To check the credit usage in your workspace:

1.  Click your account name in the corner.
2.  Go to `Settings` and then `Usage` in the sidebar.
3.  Within `Workspace`, you can view folders, workbooks, and tables sorted by their usage.

Sort the content by `Name` (alphabetically) or by number of `Credits used` by clicking the column titles. You can `Export` this content as a CSV.

### Filter and sort credit usage

The columns in this view display:

-   `Name:` The folder, workbook, or table. Click the dropdown next to a folder or workbook to see the contents.
-   `Usage:` Marked as `Recurring` when it contains recurring credit usage (e.g., scheduled runs or signals).
-   `Owner:` The person who owns the project.
-   `Credits used:` The amount of credits used for this period.

Filter any of the content on this page by:

1.  When the credits were used.
2.  Owner of the project.
3.  Specific integrations being used.

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

## **Credit usage breakdown**

The credit usage dashboard is organized into tabs, each covering a different slice of your workspace spend. Use the `When` dropdown and `Apply filters` to scope each tab to a specific time period.

-   **Workbooks** — shows credit spend broken down by folder, workbook, and table. Click the dropdown next to any folder or workbook to drill into its contents. Sort by `Name` or `Credits used`. Click `Export` to download a CSV for offline analysis.
-   **Integrations** — shows credit spend grouped by integration across your entire workspace, so you can quickly see which data providers are consuming the most credits. Sort by `Name` or `Credits used`. Click `Export` to download a CSV.
-   **Signals** — shows credit spend broken down by individual signal. A totals row (`All Signals`) appears at the top, followed by a per-signal breakdown of `Credits used` and `Actions used`.
-   **MCP** — shows programmatic spend from team members who access Clay through ChatGPT, Claude, or Glean, broken down by user. Spend that can't be attributed to a specific user appears as `Unattributed`. For per-user credit limits and live usage tracking, see `Settings → MCP users`.
-   **API** — shows programmatic spend generated through Clay's API and Exportly, broken down by user. Like MCP, unattributable spend appears as `Unattributed`.

### Reconciling your credit balance

A few things to know when comparing numbers across the dashboard:

**Each tab shows that channel's spend only.** The Workbooks, Integrations, Signals, MCP, and API tabs do not overlap — each one tracks a separate slice of your workspace activity. To calculate your total workspace credit consumption, sum the top-level totals across all tabs.

**The header popup reflects your remaining balance against your plan's credit allocation.** When you see "X / Y credits available," Y is the credit amount from your current plan (for example, 1.8M for an annual Pro plan) and X is your remaining balance. The implied consumed figure (Y − X) shows how many of your *plan credits* have been spent.

**Extra credits create a gap between the header math and your tab totals.** If your workspace has received credits beyond the plan subscription — for example, referral rewards, admin-added goodwill credits, or courtesy top-ups — those credits are added directly to your balance. When those extra credits are spent on enrichments, the usage appears in the relevant tabs (e.g., Workbooks). However, the plan-based header math (Y − remaining) does not account for those bonus credits, so it will understate actual total consumption. The difference between your tab totals and the header math is typically equal to the extra credits your workspace received and spent.

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

**Learn more:** For related information, check out our [credit limit FAQs doc](http://university.clay.com/docs/credit-spend-limits-faq).
