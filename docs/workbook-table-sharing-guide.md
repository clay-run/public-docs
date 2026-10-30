---
title: Share workbooks and tables as templates
description: Share Clay workbooks and tables as templates, keep reusable table structures, and move workbooks or folders of workbooks between workspaces.
last_synced: 2026-04-26T01:40:56.186Z
---

# Share workbooks and tables as templates

Share your Clay workbooks and tables.

In Clay, you can share tables and workbooks via a public link or specific emails. Follow these steps to share your table or workbook.

## Share a workbook or table

1.  Click on your workbook's title to access workbook settings. If you're sharing a table, click on the table's title or locate the table settings icon in the bottom right corner.
2.  Scroll to the bottom and toggle on `Share as Template`.
3.  Copy the public link to share the template with anyone or share with specific emails.

Note that when sharing as a template, only the table structure and one row of sample data are shared. If you need to share your table data, you can export the table as a CSV file.

**Table limit:** By default, workbooks with more than 10 tables cannot be duplicated or shared as templates. If your workbook exceeds this limit, contact Clay support to have the limit raised for your workspace.

## Keep a reusable table structure

**Share as Template** generates a public link that anyone can use to copy your table structure into their workspace. If you want a private, reusable starting point without creating a public link, you can duplicate the table and move the copy to a dedicated workbook:

1. Right-click the table on the workspace homepage (or open the table's title menu) and select **Duplicate table**.
2. Click the duplicate's title and select **Move to workbook** to place it in a separate workbook you use as a template library.

Duplicating copies the table structure, column definitions, and run settings but not enriched row data, so the copy starts empty and ready to use. Whenever you need a fresh working copy, duplicate from this table.

**Tip:** Add `[Template — Do Not Delete]` to the table name to make it clear which table should be duplicated rather than edited directly.

## Move a workbook to a different workspace

You can use Share as Template to copy a workbook into any workspace you have access to — including a different workspace under the same login.

### Same login, different workspaces

1. Open the workbook in the source workspace.
2. Click the workbook title, scroll to **Share as Template**, toggle it on, and copy the link.
3. Make sure your account is already a member of the destination workspace. If not, add yourself via the workspace's member settings first.
4. Open the template link in your browser. If you have access to multiple workspaces, Clay will prompt you to choose which workspace to create the workbook in. Select the destination workspace and create the workbook.

Tables, columns, formulas, and enrichment column configurations all copy over. Audiences and credits stay tied to the original workspace and are not transferred.

**Row data does not transfer.** The template link copies only the table structure and one row of sample data — your existing rows are not included. To bring your row data to the new workspace, export each table as a CSV from the source workspace, then import those CSVs into the corresponding new tables. When prompted during import, choose **Save and don't run** to avoid re-triggering enrichments on the imported rows.

**Lookup Rows and Send Table Data columns:** When you copy a whole workbook with a template link, Lookup Rows and Send Table Data columns that point to another table *in the same workbook* are reconnected automatically to the new copy of that table in the destination workspace. Columns that point to a table *outside* the workbook arrive in the new workspace with no target table configured — open each of those columns and point it at the correct table in the new workspace. If you share a single table as a template instead of the whole workbook, every Lookup Rows column in the copied table arrives with no target table and must be reconfigured.

### Move multiple workbooks or a whole folder to another workspace

Clay has no bulk, folder-level, or backend transfer for moving workbooks between workspaces, and Clay support can't move them for you. Folders can't be shared as templates, so to move a folder of workbooks, repeat the Share as Template steps above for each workbook in the folder, then export and import the row data for each table as a CSV.

To keep the number of template links low, share each workbook as a whole rather than sharing its tables one at a time — copying the whole workbook also keeps Lookup Rows and Send Table Data connections between its tables.

**Workbooks with more than 10 tables:** By default, a workbook with more than 10 tables can't be shared as a template. A workbook with exactly 10 tables can be shared. If you try to share a larger workbook, Clay shows an error like "Shared workbooks can have a maximum of 10 tables. This workbook has 14 tables." To move a workbook like this, either split its tables into smaller workbooks of 10 tables or fewer before sharing, or contact Clay support to have the limit raised for your workspace.

### Separate Clay accounts (different logins)

There is no native one-click migration between two unrelated Clay accounts. The recommended approach:

1. Share each workbook as a template to recreate the table structure in the new account.
2. Export each table's row data as a CSV from the source workspace.
3. Import those CSVs into the corresponding new tables in the destination account. When prompted, choose **Save and don't run** to import the rows without triggering enrichments — this prevents enrichment columns from re-running on every imported row and consuming credits. If you want to permanently prevent auto-run on future additions as well, turn off **Auto-run** in the table settings before importing. See [Auto-run](auto-run.md) for details.
4. Reconnect any integrations and reconfigure enrichment columns that reference connections from the source workspace.

**Lookup Rows and Send Table Data columns:** As with moving between workspaces under the same login, Lookup Rows and Send Table Data columns that point to another table in the same workbook are reconnected automatically when you copy the whole workbook. Columns that point to a table outside the workbook arrive in the new account with no target table configured. After rebuilding all tables in the destination account, open each of those columns and point it at the correct migrated table.

### Billing when consolidating two workspaces

Each Clay workspace has its own plan and bills independently — there is no automatic billing merge. Consolidating two workspaces means keeping one plan and canceling the other.

Once you have moved all workbooks and data to the workspace you're keeping:

1. Verify everything you need is accessible in the destination workspace.
2. Go to **Settings → Plans & billing** in the workspace you're leaving.
3. Select **Cancel plan** to cancel its subscription.

**Credits and plan features do not transfer between workspaces.** If the workspace you're leaving has unused data credits, spend them before canceling — when a plan is canceled, the credit balance is capped at the Free plan's rollover limit (200 credits), and any credits above that are forfeited. See [Plans & billing](plans-and-billing.md) for details on how cancellation affects your credit balance.
