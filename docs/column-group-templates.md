---
title: Column group templates
description: Column group templates are deprecated. Use functions to save and reuse enrichment workflows across your workspace.
last_synced: 2026-04-26T01:39:46.520Z
---

# Column group templates

**Note:** Column group templates are deprecated. The **Save as template** option has been removed from the column right-click menu — use **Save as function** instead. Functions provide the same reusable-column capability with added permission handling and observability, and can be called from any product surface area. See [Functions](functions.md) to get started. Existing column group templates continue to work, and you can migrate them to functions using the built-in migration workflow described below.

## Grouping columns

You can group related columns together in a table to keep your workspace organized. Grouped columns appear under a shared header that you can collapse or expand to show or hide the columns within.

To group columns:

1.  While in a table, select multiple columns by clicking their header while holding `⌘` (Mac) or `ctrl` (Windows) on your keyboard.
2.  Right-click one of the selected headers.
3.  Select **Group X columns** from the menu.

Once grouped, click the arrow on the group header to collapse or expand the columns in the group. To ungroup columns or rename the group, click the group header to open the group settings panel.

To add a new column to an existing group, open the dropdown menu for any column already inside the group and choose **Insert right** or **Insert left**. The new column is added to the same group, adjacent to the column you selected. If the group is collapsed when you insert, the new column is placed outside the group instead.

## Using a column group template

When you open an existing column group template, a **Function migration** notice appears at the top of the configuration panel. The notice reads: "Recipes no longer receive active maintenance. We recommend using functions for reusable enrichment." It includes a **Migrate to function** button that walks you through converting your template into a function. You can also reach this migration workflow from the command center or enrichment panel by clicking the settings icon next to the template name.

Public column group templates are no longer shown in the enrichment panel or command center. Only templates you created in your own workspace are available.

1.  While in a table, click `Tools`.
2.  Search for your template by name, or click **View all enrichments** and select the **Templates** tab.
3.  Click the template to open the configuration panel.
4.  Under **Configure**, map the template's required inputs to your existing table columns.
5.  Under **Providers**, connect any integrations the template requires.
6.  Click **Save** to add the columns to your table.

**About integration accounts:** Column group templates do not include the template creator's integration credentials. When you apply a template, Clay automatically connects integration columns to an account you have already set up in your workspace. If your workspace does not yet have that integration connected, the columns are added but show a **Required auth account is missing** error. To fix this, open each affected column's settings, select or add your integration account in the account selector, and click **Save**.

## Editing a column group template

A column group template stores a snapshot of your column configuration at the time it was saved. If you later change a column's prompt, model, or other settings, those changes do not automatically update the template.

You can update a template's name, description, and category from the template library:

1.  While in a table, click `Tools`.
2.  Search for your template by name or click **View all enrichments** and select the **Templates** tab to find your template.
3.  Click the `...` menu next to the template and select **Edit template settings...**.
4.  Update the details and click **Save**.

## Deleting a column group template

1.  While in a table, click `Tools`.
2.  Search for the template name or click **View all enrichments** and select the **Templates** tab to find the template you want to delete.
3.  Click the `...` menu next to the template.
4.  Select **Delete**.
5.  Click **Delete template** to confirm.

Deletion is permanent and cannot be undone.
