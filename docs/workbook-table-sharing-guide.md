---
title: Share workbooks and tables as templates
source_url: https://university.clay.com/docs/workbook-table-sharing-guide
description: Share Clay workbooks and tables as templates, and move workbooks between workspaces.
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

## Use a shared template

When someone shares a template link with you, opening it creates a **new workbook** — you cannot apply a template to an existing empty table or sheet.

To create a workbook from a template:

1. Open the template link in your browser.
2. If you have access to multiple workspaces, Clay will prompt you to choose which workspace to create the workbook in. Select the workspace and confirm.
3. Clay creates a fresh workbook containing the template's table structure and sample data.

You can then rename the workbook, clear the sample row, and start adding your own data.

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
