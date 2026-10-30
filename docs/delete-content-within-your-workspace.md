---
title: Delete content within your workspace
description: Learn how to delete and recover tables, workbooks, and rows within your workspace, and how to delete people from Audiences for data privacy requests.
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

After that alert closes, there is no self-serve way to recover deleted rows. The Clay support team may be able to restore deleted rows within **30 days** of deletion, but recovery is **not guaranteed** — whether the data can be restored depends on the situation, and support can only confirm after investigating your specific case. To request row restoration, reach out to support and share:

-   Your table URL
-   Approximately when the rows were deleted

Note: rows cannot be restored if doing so would put your table over the 50,000-row limit.

## Cell data cannot be recovered

Recovery only applies to deleted rows — **individual cell data cannot be recovered**, by you or by Clay support. If a cell's value is cleared or overwritten (for example, by clearing a cell, editing its contents, or re-running an enrichment that returns a different result), the previous value is gone. [Table versions](table-versions.md) do not help here either: they capture your table's structure and configuration, not cell data.

## Request deletion of records for data privacy compliance

If your end-customers request that their data be deleted — for example, under GDPR or CCPA — and that data has been processed in Clay (imported from a source, enriched, or stored in a table or audience), you have two options:

-   **People stored in Audiences:** Delete them yourself with the Clay public API. See [Delete people from Audiences with the Clay public API](#delete-people-from-audiences-with-the-clay-public-api).
-   **Any other data in Clay** (tables, source imports, or a full workspace): Submit a formal deletion request to Clay's Privacy team, as described below.

**Important:** Disabling a source sync prevents future records from being imported but does not remove data that has already been imported into Clay. To have existing records removed, you must submit a deletion request.

**Before submitting, gather the following:**

-   Your Clay workspace URL or ID
-   The specific records to be deleted, including identifiers such as email addresses, external IDs, or profile URLs
-   The relevant Clay table, audience, or data source
-   Whether you are requesting deletion of specific records, an entire source import, or the full workspace
-   Confirmation that the records have also been deleted or suppressed in the original source system, so they are not re-imported

**How to submit:**

Email **privacy@clay.com** or contact your Clay Growth Strategist. Clay's Privacy team will review the request, determine the appropriate deletion scope, and coordinate any required deletion actions in Clay or with relevant third-party providers.

Requests are generally processed within 30 days. If additional information is needed, the Privacy team will follow up.

### Delete people from Audiences with the Clay public API

Audiences privacy deletion lets you hard delete people from Audiences yourself through the Clay public API, so you don't have to email the Privacy team. A privacy deletion permanently removes every record of each matching person from all Audiences databases in one workspace: the workspace your API key belongs to. Deleted records can't be recovered.

**Requirements for Audiences privacy deletion:**

-   Audiences enabled on your workspace
-   A workspace-scoped Clay public API key. See [How to find your Clay API key](guide-find-clay-api-key.md).
-   Workspace admin permissions

**To delete people from Audiences:**

1.  Send a `POST` request to `/audiences/privacy-delete` with the people you want to delete. You can include up to **100** people per request and identify each one by **email address** or **LinkedIn slug**. A LinkedIn slug is the handle at the end of the profile URL, not the full URL.
2.  If any people match, Clay queues the deletion and returns a `job_id` with the status `in_progress`. If no people in the workspace match your identifiers, the status is `no_matches` and nothing is deleted.
3.  To track the deletion, send a `GET` request to `/audiences/privacy-delete/{job_id}`. The status stays `in_progress` while the job is queued, running, or retrying. It changes to `complete` when the deletion finishes, or `failed` if it couldn't finish.

Clay automatically retries Audiences privacy deletion jobs that hit an error, so a job showing `in_progress` for a while is still being worked on.

For the full request and response reference, see [Privacy delete people from Audiences](https://developers.clay.com/api-reference/audiences/privacy-delete-people-from-audiences) and [Get Audiences privacy deletion status](https://developers.clay.com/api-reference/audiences/get-audiences-privacy-deletion-status).

**Note:** Audiences privacy deletion only removes data from Audiences. To delete the same people from Clay tables or other data, submit a deletion request to the Privacy team as described above. Also delete or suppress the records in your original source system (for example, your CRM) so a future sync doesn't import them again.
