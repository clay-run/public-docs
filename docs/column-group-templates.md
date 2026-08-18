---
title: Column group templates
description: Apply, edit, and delete existing column group templates; use Save as function to create new reusable column sets across your workspace.
last_synced: 2026-04-26T01:39:46.520Z
---

# Column group templates

Column group templates let you save and reuse related column sets across tables in your workspace.

**Creating new column group templates using "Save as template" has been replaced by [Functions](functions.md).** To save a set of columns for reuse across tables, select the columns, right-click one of the selected headers, and choose **Save as function** instead. Functions provide the same column reusability with additional capabilities: logic updates everywhere at once when you edit the function, permissions control, and observability. Functions are available on all paid plans. See [Functions](functions.md) for step-by-step instructions.

> **Note:** This change is rolling out across workspaces. If you still see a **Save as template** option in your multi-column right-click menu, your workspace may not yet have received the update — **Save as function** is the supported replacement going forward. Contact support if you have questions about your workspace.

If you have existing column group templates, you can still apply, edit (name and description only), and delete them as described below. To convert an existing template into a function, open the template from **Tools → Templates** and use the migration workflow shown in the template's settings panel.

## Grouping columns

You can group related columns together in a table to keep your workspace organized. Grouped columns appear under a shared header that you can collapse or expand to show or hide the columns within.

To group columns:

1.  While in a table, select multiple columns by clicking their header while holding `⌘` (Mac) or `ctrl` (Windows) on your keyboard.
2.  Right-click one of the selected headers.
3.  Select **Group X columns** from the menu.

Once grouped, click the arrow on the group header to collapse or expand the columns in the group. To ungroup columns or rename the group, click the group header to open the group settings panel.

To add a new column to an existing group, open the dropdown menu for any column already inside the group and choose **Insert right** or **Insert left**. The new column is added to the same group, adjacent to the column you selected. If the group is collapsed when you insert, the new column is placed outside the group instead.

To save a group of columns for reuse in other tables, see [Functions](functions.md).

## Using a column group template

Existing column group templates you have already created can still be applied to tables:

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

To update the column logic in a template, convert the template to a function: apply the template to a table, edit the columns as needed, then save them as a function via **Save as function** (see [Functions](functions.md)).

## Deleting a column group template

1.  While in a table, click `Tools`.
2.  Search for the template name or click **View all enrichments** and select the **Templates** tab to find the template you want to delete.
3.  Click the `...` menu next to the template.
4.  Select **Delete**.
5.  Click **Delete template** to confirm.

Deletion is permanent and cannot be undone.
