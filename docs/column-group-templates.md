---
title: Column group templates
description: Create, apply, and edit column group templates to reuse related column sets across your workspace.
last_synced: 2026-04-26T01:39:46.520Z
---

# Column group templates

Save columns into templates to easily reuse them.

Column group templates let you save and reuse related column sets across tables in your workspace. This eliminates the need to recreate complex column configurations repeatedly, saving time and maintaining consistency.

Instead of rebuilding multi-column setups manually, you can apply saved templates quickly, helping you focus on your data rather than table structure.

## Grouping columns

You can group related columns together in a table to keep your workspace organized. Grouped columns appear under a shared header that you can collapse or expand to show or hide the columns within.

To group columns:

1.  While in a table, select multiple columns by clicking their header while holding `⌘` (Mac) or `ctrl` (Windows) on your keyboard.
2.  Right-click one of the selected headers.
3.  Select **Group X columns** from the menu.

Once grouped, click the arrow on the group header to collapse or expand the columns in the group. To ungroup columns or rename the group, click the group header to open the group settings panel.

To save a group of columns so you can reuse it in other tables, see [Creating a column group template](#creating-a-column-group-template) below.

## Creating a column group template

1.  While in a table, select multiple columns by clicking their title while holding `⌘` (Mac) or `ctrl` (Windows) on your keyboard.
2.  `Right-click` on one of the titles and select `Save as template`.
3.  Write a name and other details so your template is easier to find later.
4.  Click `Create template`.

## Using a column group template

1.  While in a table, click `Add enrichment`.
2.  Select `Templates` and search for your template.
3.  Click the template to open the configuration panel.
4.  Under **Configure**, map the template's required inputs to your existing table columns.
5.  Under **Providers**, connect any integrations the template requires.
6.  Click **Save** to add the columns to your table.

## Editing a column group template

You can update a template's name, description, and category from the template library:

1.  While in a table, click `Add enrichment`.
2.  Select `Templates` and find your template.
3.  Click the `...` menu next to the template and select **Edit template settings...**.
4.  Update the details and click **Save**.

To update the columns in a template, you need to recreate it:

1.  Apply the template to a table (or use an existing table where it was applied).
2.  Edit the columns in the table as needed.
3.  Select the updated columns by holding `⌘` (Mac) or `ctrl` (Windows) and clicking each column title.
4.  `Right-click` on one of the selected titles and select `Save as template`.
5.  Enter a name and click `Create template`.
