---
title: Sources
source_url: https://university.clay.com/docs/sources
description: Every Clay table begins with a source. Sources are the foundation
  of how data gets into your tables.
last_synced: 2026-04-26T01:40:43.486Z
---

# Sources

Every Clay table begins with a source. Sources are the foundation of how data gets into your tables.

Sources are the foundation of Clay and determine how data flows into your table—think of them as the roots of a tree feeding information into your database. Just like a tree needs strong roots to grow and thrive, every Clay table needs well-configured sources to function effectively.

Every Clay table starts with a source. You can import customer data from a CSV file, connect to your CRM system, or receive real-time updates through webhooks. Sources are your gateway to organizing and managing data in Clay.

## Types of sources

-   List builders ([Find Companies](https://www.clay.com/university/guide/find-companies), [Find People](https://www.clay.com/university/guide/find-people-overview))
-   CRM systems ([Hubspot](https://www.clay.com/university/guide/hubspot-integration-overview), [Salesforce](https://www.clay.com/university/guide/salesforce-integration-overview))
-   [Webhooks](https://www.clay.com/university/guide/webhook-integration-guide)
-   [CSV files](https://www.clay.com/university/guide/csv-import-overview)

## Adding sources to table

**Add to a new table:**

1.  Click `+ Add` at the bottom of a workbook to create a new table.
2.  Search for and select your desired data source (such as Salesforce or Find People).
3.  Configure the source settings.
4.  Review the preview and click `Import to new table`.

**Add to an existing table:**

1.  In a table, click `Tools` → `Import`.
2.  Search for and select your desired data source (such as Salesforce or Find People).
3.  Configure the source settings.
4.  Review the preview and click `Import`.

### Importing CSV

**To import a CSV file into a new table:**

1.  Click `+ Add` at the bottom of a workbook to create a new table.
2.  Click `Import from CSV` and select your file.
3.  Click `Complete import`.

**To import to an existing table:**

1.  In a table, click `Tools` → `Import`.
2.  Click `Import from CSV` and select your file.
3.  Select and map columns from your CSV to the Clay table.
4.  Click `Add to table`.

## Importing accounts and contacts together

The recommended setup for working with both companies and people in Clay is two linked tables in the same workbook — one for accounts/companies and one for contacts/people.

### Step 1: Create your accounts table

1.  In a new workbook, click `+ Add` at the bottom to create your first table.
2.  Add your company/account data using one of these sources:
    -   **CSV:** Select `Import from CSV` and upload your accounts file.
    -   **Salesforce or HubSpot (live sync):** Search for `Salesforce` or `HubSpot`, select the accounts/companies object, and configure the connection.

### Step 2: Create your contacts table

Click `+ Add` again to add a second table for your contacts/people. The same source options apply:

-   **CSV:** Select `Import from CSV` and upload your contacts file.
-   **Salesforce or HubSpot:** Select the contacts/people object from your CRM.
-   **Find People:** Use the `Find People` source to search Clay's database for contacts matching your criteria.

### Step 3: Link contacts to their accounts

How the link is created depends on which source you used for contacts:

**If you used Find People at These Companies** (launched from your accounts table): A **Company Table Data** column is automatically added to the contacts table, linking each person back to their company row. No additional setup is required.

**If you imported contacts from CSV or CRM:** Add a **Lookup Rows** action on the contacts table to pull account-level data into each contact row:

1.  In your contacts table, click `+ Add column` and select `Lookup single row in other table`.
2.  Set `Table to search` to your accounts table.
3.  Set `Target column` to your match key in the accounts table (typically **company domain** or **Account ID**).
4.  Set `Row value` to the corresponding column in your contacts table.
5.  Run the lookup.

This gives you account-level attributes (company name, industry, revenue, etc.) directly on each contact row. For more details on configuring lookups, see [Lookup Rows](https://university.clay.com/docs/lookup-rows).

### Tips for CRM imports

-   **Scope your source before the first sync.** When connecting Salesforce or HubSpot, use a pre-filtered list view or segment (e.g., filtered by account stage, owner, or segment) as your source. This ensures you bring in only the records you plan to work with — not your entire CRM.
-   **Sources are additive.** Once records are imported, narrowing your source filter does not remove rows already in the table. See [Will rows already in my table be removed if they no longer match the source filter?](#will-rows-already-in-my-table-be-removed-if-they-no-longer-match-the-source-filter) below.

## Modifying sources

1.  In a table, click the source column title.
2.  Click `Sources` and the name of the source.
3.  Click `Edit source` and adjust the settings as needed.

## Deleting sources

1.  In a table, click the source column title.
2.  Click `Sources` and the name of the source.
3.  Click `Delete source`.

## Scheduled sources

Scheduling source runs is one of the most powerful features, as it keeps your information automatically up to date. To learn more, check out [scheduled sources](https://www.clay.com/university/guide/scheduled-sources).

## FAQs

### Why is the Submit button greyed out when configuring the "Find local businesses using Google Maps" source?

**The Submit button stays disabled until all required fields are filled in — including fields that appear dynamically after you make a selection.**

When you choose a **Search Type** (either **Business types** or **Free text**), a new required field appears directly below it. Because this field loads below the visible area of the dialog, it's easy to miss.

To fix this:

1.  After selecting a search type, **scroll down** inside the source configuration dialog.
2.  Fill in the required field that appeared:
    -   If you selected **Business types**: choose at least one business type from the dropdown.
    -   If you selected **Free text**: enter a search query (for example, "coffee shops" or "HVAC contractors").
3.  Once all required fields are filled, the Submit button will become clickable.

### Why doesn't my Clay table update when I change the source filters?

**Editing the source of a Clay table after it's been run won't retroactively update the results, because Clay doesn't reprocess previously generated data automatically.**

Even if the source preview shows the new filters, the table won't refresh until you explicitly re-run the source. Rows already in the table **stay** — they are not automatically removed if they no longer match the updated filters (for example, companies that were part of a HubSpot list but have since been excluded by a filter change).

To control which rows are in your table after updating source filters, you have two options:

-   **Remove specific rows manually:** Apply a table filter to isolate rows you no longer want, select them, and delete them. This preserves the rest of your table without re-running the source.
-   **Reset the table to match current filters:** Delete all existing rows and re-run the source (or duplicate the table with the updated source). This clears the table and re-imports only records that match the current source filters.

### Will rows already in my table be removed if they no longer match the source filter?

**No. Clay sources are additive only — they add rows (and optionally update them), but they never automatically remove rows from your table.**

If you narrow a source filter — for example, by updating a HubSpot list or segment so that certain contacts or companies no longer qualify — the rows already in your Clay table will stay. They are not deleted automatically.

The **Update existing rows** toggle (available when re-running a source) controls whether Clay refreshes the data in existing rows on re-run. It does not remove rows that are no longer included in the source.

To remove rows that no longer match your filter, you have two options:

-   **Delete them manually** — select the rows in the table and delete them.
-   **Delete and re-run the source** — this re-imports records based on the current filter. You will need to clear any previously imported rows first if you want a clean slate.

### I am trying to add a source to an existing table, but I get an error

When adding a new source to an existing table, you must have the appropriate columns set up. For example, to add a `Find company` source, you need professional social URLs or Company Domains columns.

### **What are the row limits for Clay tables and sources?**

Clay tables have a **50,000-row limit** across all plans. This applies to all sources including CSV files, CRM systems, list builders, webhooks, and signals.

**Source-specific limits:**

-   **Salesforce Reports**: 2,000 records (API restriction)
-   **Salesforce List Views**: 50,000 records
-   **All other sources**: 50,000 records

**What happens when you hit the limit?**

Clay imports records up to the limit and stops automatically. No error message is displayed.

**Solutions for large datasets:**

-   Split your data using filters or date ranges into multiple tables
-   Use [auto-delete](https://university.clay.com/docs/table-management-settings#auto-delete-passthrough-tables) (Enterprise plan) for unlimited rows
-   Use [bulk enrichment](https://www.clay.com/university/guide/bulk-enrichment) (Enterprise plan) to process millions of records
