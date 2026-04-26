---
title: Credit usage
source_url: https://university.clay.com/docs/credit-usage
description: Track credit consumption across your workspace.
last_synced: 2026-04-26T01:39:49.092Z
upstream_hash: d554b6234917090eecbf1c6c7c3d5a74bba6b86bf7d2a8a6938802d685d741ec
---

# Credit usage

Track credit consumption across your workspace.

Track, analyze, and optimize your credit consumption by breaking down usage across workbooks, tables, and integrations.

## Credit usage dashboard

To check the credit usage in your workspace:

1.  Click your account name in the corner.
2.  Go to `Settings` and then `Credit usage` in the sidebar.
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

**Note:** Historical data for the table credit dashboard begins on November 5th, 2025. You’ll see a warning about incomplete data if your selected time range begins before this date.

**How to access the table dashboard:**

_From a table:_

-   Click the `Credit usage` button within the Credits popover and select `Table credit usage`.
-   Click the `Table History` button in the lower right corner of your table.

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

**Note:** Historical data for the table credit dashboard begins on November 5th, 2025. You’ll see a warning about incomplete data if your selected time range begins before this date.

## Credit usage by integration

To view which integrations are using the most credits, click `Integrations` in the top bar next to `Workspace`.

Sort the content by `Name` (alphabetically) or by number of `Credits used` by clicking the column titles. You can `Export` this content as a CSV.

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
