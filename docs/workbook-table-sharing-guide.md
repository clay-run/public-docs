---
title: Share workbooks and tables as templates
description: Share Clay workbooks and tables as templates, keep reusable table structures, and move workbooks between workspaces.
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

### Separate Clay accounts (different logins)

There is no native one-click migration between two unrelated Clay accounts. The recommended approach:

1. Share each workbook as a template to recreate the table structure in the new account.
2. Export each table's row data as a CSV from the source workspace.
3. Import those CSVs into the corresponding new tables in the destination account.
4. Reconnect any integrations and reconfigure enrichment columns that reference connections from the source workspace.
