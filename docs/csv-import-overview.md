---
title: How to import your CSV into Clay
description: Import your CSV into Clay.
last_synced: 2026-04-26T01:39:49.725Z
---

# How to import your CSV into Clay

Import your CSV into Clay.

Within Clay you can import CSV as a source to an existing or new table.

## Importing a CSV into Clay

1.  Open the source panel:
    -   **For a new table:** From your workspace home, click `+ Create new` and search for `CSV`.
    -   **For an existing table:** Open the table, click `Tools` and select `Import`.
2.  Upload your file by clicking `Browse Files` or dragging and dropping your CSV into the upload area.

    > **Note:** If your CSV has more rows than your plan allows in a single table, the upload dialog will either block the import with an error or show an **"Import First N Rows"** button that imports only up to your plan's limit. If you see fewer rows than expected after importing, you've likely hit your plan's row limit — upgrade your plan or contact Clay support to increase it.

3.  Select your destination:
    -   `Add to current table` — appends the CSV rows to your existing table.
    -   `Create new table` — creates a new table populated with your CSV data.
    -   `Replace current table` — overwrites the current table's rows with the CSV data.

    > **Note:** None of these options update existing rows. `Add to current table` always appends each CSV row as a new row — it does not match records by a column value or update rows that already exist in your table. If you need to add a column's values to rows that are already in Clay (for example, a "Keep/Remove" status matched on LinkedIn URL), see [Adding a new column to existing rows](#adding-a-new-column-to-existing-rows) below.

4.  Map your CSV columns to the correct Clay table fields.
5.  Choose how to handle the imported rows:
    -   `Save and run rows in this CSV` — imports the rows and immediately queues all enrichment columns to run on every imported row. If your table has enrichment columns configured (email finders, waterfalls, AI columns, etc.), they will all fire and consume credits.
    -   `Save and don't run` — imports the rows without triggering any enrichments for this batch. This is a one-time skip for the current import only — it does not change your table's [Auto-run](table-management-settings.md) setting.

    > **Tip:** If you're importing into a table that already has enrichment columns and you don't want them to run on the new rows, choose `Save and don't run`. If you want to prevent enrichments from automatically running on all future row additions as well, turn off **Auto-run** in your [table settings](table-management-settings.md) before importing.

## Next steps after importing

Once your data is in Clay, you can enrich rows to pull in additional information.

**If you imported a list of companies and want to find contacts and their email and phone numbers:**

1.  **Find company domains (if your list has company names but no domains).** The Work Email waterfall requires a company domain for each row — a company name alone is not enough. In your table, click **Tools**, switch to the **Enrich** tab, and search for **Company Domain** to add the Company Domain waterfall. Map the column containing company names as the input and click **Save**. The waterfall cascades across multiple providers to find a domain, stopping as soon as one returns a result.
2.  **Find contacts at each company.** Click **Tools**, switch to the **Import** tab, and select **Find People at These Companies** to search for people at each company by job title, seniority, or other criteria. Each match is returned as a separate contact row.
3.  **Add email and phone enrichments to the contacts table:**
    -   **Work email:** Click **Add enrichment**, search for **Work Email**, and select the waterfall. It requires each person's full name and company domain.
    -   **Mobile phone:** Click **Add enrichment**, search for **Phone number**, and select the waterfall under **Waterfalls**. It requires the person's professional profile URL, which is returned by the people search.

Importing a company list does not automatically add contact rows, emails, or phone numbers — you need to run these steps explicitly. Once enrichments are configured, Clay auto-runs them on any new records added to your table. For full setup instructions, see [Finding companies and people in Clay](finding-companies-and-people-in-clay.md), [Work Email waterfall](work-email-waterfall.md), and [Waterfalls](building-a-data-waterfall.md).

**If your CSV already has partial data and you want to verify or fill in only what's missing:**

When you import a CSV that already contains some fields — such as email addresses, LinkedIn URLs, or company names — you do not need to re-enrich everything from scratch. Use **run conditions** on each enrichment column to skip rows that already have data, so you only spend credits on rows that actually need it.

-   **To validate emails you already have:** Add a column → `Tool` → search for **Validate Email** → map the input to your existing email column. In **Run settings**, set the condition to `/Email is not empty` (replace `Email` with your actual column name). The tool runs only on rows that have an email; rows without one are skipped and no credits are consumed.

-   **To find emails only where they're missing:** Add a column → `Tool` → search for **Work Email Waterfall** → map the inputs (LinkedIn URL, first name, last name, company). In **Run settings**, set the condition to `/Email is empty`. The waterfall only runs on rows that don't yet have an email, leaving rows that already have one untouched.

-   **The same pattern applies to any field:** to enrich a column only where the current value is blank, set the run condition to `/ColumnName is empty`. Rows where the condition is not met show **"Run condition not met"** and consume no credits — even when you click **Run all rows**.

For a full reference on run condition syntax, see [Conditional runs](conditional-runs.md).

**If you want to add a new column's values to existing rows using a shared identifier:**

CSV import cannot update rows that already exist in Clay — there is no upsert mode. If you have a spreadsheet with new column values to bring into your existing Clay table (for example, a "Keep/Remove" status column matched on LinkedIn Profile URL), use this two-step approach instead:

1.  Import the enriched CSV as a **new** Clay table (choose `Create new table` at step 3 above).
2.  In your original table, click **Add enrichment** and search for **Lookup Single Row in Other Table**.
3.  Set the matching column (e.g., LinkedIn Profile URL) so Clay finds the right row in the new table.
4.  Map the column you want to populate (e.g., "Keep/Remove\") as an output.

Each existing Clay row fetches the matching value from the new table without creating duplicates.

## Troubleshooting CSV field issues

**If columns appear mixed up or data lands in the wrong fields:**

Clay auto-detects the separator character (delimiter) used in your CSV. Supported separators are comma (`,`), semicolon (`;`), tab, and pipe (`|`). Clay samples the file and picks the separator that appears most consistently across rows.

Fields can end up in the wrong columns when:

-   **The file mixes separator characters.** If some rows use commas and others use semicolons as the separator, Clay picks one for the whole file and the rows using the other separator will misparse. Each CSV should use a single, consistent separator throughout.
-   **Data values contain the separator character without quoting.** If your separator is a comma and a field value also contains a comma — for example, a company name like `Smith, Jones & Co.` — the parser may split that value into two separate fields. Wrap such values in double quotes (`"Smith, Jones & Co."`) or remove the separator character from the value before importing.

To confirm which separator your file uses, open it in a plain text editor. Once you've identified it, check that no data values contain that same character without surrounding double quotes.

**If your upload is blocked because the file is too large:**

Clay's CSV import supports a maximum of **100 columns** and **50,000 rows** per file by default. Uploads that exceed either limit are rejected before the import can proceed. If your file exceeds the column limit, remove any columns you don't need before uploading; if it exceeds the row limit, split it into smaller batches. If your workspace has a lower column limit configured by Clay support, the error will appear at that threshold instead.

**If your upload fails with an encoding error:**

Clay requires **UTF-8 encoded** CSV files. Files saved with other encodings (such as Latin-1 or Windows-1252) will produce garbled output or fail to import. When exporting from a spreadsheet tool, look for a "UTF-8" or "CSV UTF-8" save option. If you are unsure of your file's encoding — or if the upload fails for no obvious reason — paste your data into a Google Sheet and download it as a CSV (`File → Download → Comma-separated values`). Google Sheets exports UTF-8 by default and also strips hidden formatting artifacts and inconsistent line endings that can cause upload failures. After downloading the cleaned file, try the import again.

**If the upload still fails after the steps above:**

Make sure your CSV file name is short. Long file names can interfere with the upload process. Rename the file to a brief descriptive name and try again.
