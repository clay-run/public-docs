---
title: Column group templates
description: Column group templates are deprecated in favor of functions. Learn
  what changed and how to migrate an existing template to a function.
last_synced: 2026-04-26T01:39:46.520Z
---

# Column group templates

**Column group templates are deprecated.** [Functions](functions.md) have replaced them as the way to save and reuse enrichment logic across your workspace. Functions store reusable logic the same way templates did, but can be called from more places than just tables and add capabilities templates never had, such as permission handling and observability.

## What changed

-   **You can no longer create new column group templates.** The **Save as template** option in the column right-click menu has been replaced by **Save as function**. See [Creating a function](functions.md#creating-a-function).
-   **Existing templates can still be applied**, but when you open a template's configuration panel you'll see a notice at the top with a one-click workflow to migrate that template to a function (see below).
-   **Public (Clay-built) column group templates** are no longer shown in the enrichment panel or Command Center. Clay-managed functions cover the same use cases.
-   **The table template library** that previously appeared in workbook overview tabs has been removed.

Single-column action templates — for example, saving a **Use AI** or **HTTP API** column configuration as a template — are a separate feature and are not affected by this deprecation.

## Migrating a template to a function

If you have existing column group templates, you can convert each one to a function in a few clicks:

1.  Open the template's configuration panel — either by applying the template in a table, or by clicking the settings for the template from the enrichment panel or Command Center.
2.  A notice at the top of the panel explains that templates are deprecated. Click the migration button in the notice.
3.  Follow the guided workflow to create a function from the template.

Once migrated, the function appears under the **Functions** tab on your Clay homepage and can be called from any table. See [Functions](functions.md) for how to call, edit, and manage it.

To save a new set of columns for reuse going forward, select the columns, right-click, and choose **Save as function** instead.

## Grouping columns

Grouping columns within a table is unaffected by this deprecation. You can still group related columns together to keep your workspace organized — grouped columns appear under a shared header that you can collapse or expand to show or hide the columns within.

To group columns:

1.  While in a table, select multiple columns by clicking their header while holding `⌘` (Mac) or `ctrl` (Windows) on your keyboard.
2.  Right-click one of the selected headers.
3.  Select **Group X columns** from the menu.

Once grouped, click the arrow on the group header to collapse or expand the columns in the group. To ungroup columns or rename the group, click the group header to open the group settings panel.

To add a new column to an existing group, open the dropdown menu for any column already inside the group and choose **Insert right** or **Insert left**. The new column is added to the same group, adjacent to the column you selected. If the group is collapsed when you insert, the new column is placed outside the group instead.

To save a group of columns so you can reuse it in other tables, save it as a [function](functions.md#creating-a-function).
