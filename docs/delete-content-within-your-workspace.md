---
title: Delete content within your workspace
description: Learn how to delete and recover tables, workbooks, and rows within your workspace.
last_synced: 2026-04-26T01:39:53.278Z
---

# Delete content within your workspace

Learn how to delete columns, workbooks, and tables within your workspace.

## Delete columns

To delete a column:

1. Click the column header to open the dropdown menu.
2. Scroll to the bottom of the menu and select `Delete`.
3. In the confirmation dialog, click **Delete column** to confirm. If the column has downstream dependencies — such as enrichments or formula columns that reference it — they will be listed in the dialog so you can review before deleting.

**Note:** Once deleted, a column is permanently removed from your table and from the columns panel — deleted columns do not go to Trash. If you still see a column in the columns panel after trying to delete it, it is likely **hidden** rather than deleted. Hidden columns appear in the columns panel with a closed-eye icon next to their name. To delete a hidden column, temporarily unhide it first, then delete it from the column header dropdown. If you need to recover a deleted column, you can restore an earlier [table version](table-versions.md) that includes it.

## Delete rows

To delete a single row, right-click anywhere on that row and choose **Delete 1 row**.

To delete multiple rows at once:

1. Click the row selector (the small checkbox on the left side of the row) to select the first row you want to delete.
2. Scroll to the last row in the range, hold **Shift**, and click its row selector. All rows between your first click and this one are selected.
3. Right-click anywhere on the selected rows and choose **Delete [N] rows**.
4. Confirm the deletion in the dialog that appears.

**Note:** Deleted rows do not go to Trash. A brief **Undo** alert appears immediately after deletion — click it to restore the rows before the alert closes. See [Recover deleted rows](#recover-deleted-rows) for options after the alert has closed.

## Delete tables and workbooks

### Within table or workbook

To delete your table, click on your table name to access the table settings dropdown. Select `Delete` and confirm.

### In your workspace

Click on `...` icon on to the right of the table you want to delete. Select `Delete` and confirm.

### Deleting workbooks

When you delete a workbook, all tables within it are deleted along with it.

## Recover deleted tables and workbooks

Once you delete a table or workbook, it will end up in your Trash. You can access Trash from the bottom left of the workspace sidebar. Deleted items are stored in Trash for **30 days**, after which they are permanently deleted. Once you open Trash you can:

-   Delete tables permanently.
-   Recover tables. You cannot edit a table in Trash unless you restore it.

**Note:** Deleting a table moves it to Trash and immediately removes its rows from your workspace row count — you do not need to take any additional action in Trash to free up that row capacity.

When you restore a table, all of your row data and column configurations are fully restored — your data comes back exactly as it was when the table was deleted.

When you restore a workbook, all of its tables are automatically restored as well.

## Recover deleted rows

If you accidentally delete a row within a table, a brief confirmation alert appears immediately after deletion — click **Undo** in that alert to restore the row before it disappears.

After that alert closes, there is no self-serve way to recover deleted rows. However, the Clay support team can restore deleted rows within **30 days** of deletion. To request row restoration, reach out to support and share:

-   Your table URL
-   Approximately when the rows were deleted

Note: rows cannot be restored if doing so would put your table over the 50,000-row limit.
