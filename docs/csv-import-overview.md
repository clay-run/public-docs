---
title: How to import your CSV into Clay
source_url: https://university.clay.com/docs/csv-import-overview
description: Import your CSV into Clay.
last_synced: 2026-04-26T01:39:49.725Z
---

# How to import your CSV into Clay

Import your CSV into Clay.

Within Clay you can import CSV as a source to an existing or new table.

## Importing a CSV into Clay

1.  Open the source panel:
    -   **For a new table:** From your workspace home, click `+ Create new` and search for `CSV`.
    -   **For an existing table:** Open the table, click `Tools`, and select `Import`.
2.  Upload your file by clicking `Browse Files` or dragging and dropping your CSV into the upload area.
3.  Select your destination:
    -   `Add to current table` — appends the CSV rows to your existing table.
    -   `Create new table` — creates a new table populated with your CSV data.
    -   `Replace current table` — overwrites the current table's rows with the CSV data.
4.  Match your CSV columns to the correct Clay table fields.
5.  Choose how to handle the imported rows:
    -   `Save and run rows in this CSV` — imports the rows and immediately runs any enrichments on them.
    -   `Save and don't run` — imports the rows without triggering any enrichments.

## Next steps after importing

Once your data is in Clay, you can enrich rows to pull in additional information.

**If you imported a list of companies and want to find contacts and their email addresses:**

1.  In your table, click **Tools** and select **Find People at These Companies** to search for people at each company by job title, seniority, or other criteria. Each match is returned as a separate contact row.
2.  On the resulting contacts table, add a **Work Email** waterfall (**Add enrichment → Work Email**) to find and validate a work email address for each contact.

Importing a company list does not automatically add contact rows or email addresses — you need to run these two steps explicitly. For full setup instructions, see [Finding companies and people in Clay](finding-companies-and-people-in-clay.md) and [Work Email waterfall](work-email-waterfall.md).
