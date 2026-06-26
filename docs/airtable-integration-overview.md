---
title: Airtable integration overview
description: Spreadsheet-like database for organizing information and building applications.
last_synced: 2026-04-26T01:39:40.638Z
---

# Airtable integration overview

Spreadsheet-like database for organizing information and building applications.

# Airtable Overview

The Airtable integration lets you sync data within your Clay table with your Airtable bases. With this integration you're able to:

-   Create records
-   Lookup records
-   Pull records
-   Update records
-   Upsert records

## Setting up Airtable and Clay

To get set up, you'll need to add your Airtable account to Clay from either the enrichment panel or the **Settings > Connections** page.

Make sure your linked Airtable account has the right level of access to the bases you want to connect with Clay.

## Available Actions with the Airtable Integration

### `Action` Create records

Create and push a new record to your Airtable directly from Clay.

**Input Fields**:

-   **Base ID** (Required): The ID for the Airtable Base you'd like to create the record in.
-   **Additional Fields**: Any other fields you want to include as part of the record.

### `Action` Lookup records

Check if a specific record exists in your Airtable.

**Input Fields**:

-   **Base ID** (Required): The ID for the Airtable Base you'd like to search within.
-   **Lookup Criteria**: Fields or criteria to define which record to look up.

### `Action` Pull records

Import rows from an Airtable table directly into Clay as your table's data source. This is the action to use when you want to bring your Airtable data into Clay as the starting point for enrichment.

**Input Fields**:

-   **Base ID** (Required): The ID for the Airtable Base you'd like to pull records from.
-   **Table ID** (Required): The specific table within the base to import.
-   **Grid View** (Optional): A specific Airtable grid view to filter which records are pulled.
-   **Limit** (Optional): Maximum number of records to import. The maximum is 50,000.

### `Action` Update records

Modify an existing record in Airtable.

**Input Fields**:

-   **Base ID** (Required): The ID for the Airtable Base you'd like to update.
-   **Record ID**: The unique ID of the record to update.
-   **Fields to Update**: Specify the fields and values to modify.

### `Action` Upsert records

Create or update a record in Airtable based on matching values.

**Input Fields**:

-   **Base ID** (Required): The ID for the Airtable Base where you want to perform the upsert.
-   **Match Criteria**: Fields to match for determining whether to insert or update.
-   **Fields to Include/Update**: Specify fields and values to include in the operation.

## Working with Airtable linked record fields

Airtable supports **linked record** fields that reference rows in another table — for example, a Leads table where each lead is linked to a row in an Organizations table. In Airtable's UI, these fields show the linked record's name. However, Airtable's API stores and returns the underlying **record ID** (a string like `recXXXXXXXXXXXXXX`), not the human-readable name.

When Clay pulls data from Airtable — via the Pull Records source action or a Lookup Records action — linked record fields come through as **arrays containing one or more record IDs**, not as names. This is expected: Clay returns exactly what Airtable's API provides.

### Resolving a linked record ID to its name

To get the display name (or any other field) from a linked record, add a second **Lookup Record** action column that looks up the linked table by record ID:

1. Add a new enrichment column and select the **Airtable › Lookup Record** action.
2. Set **Base ID** to the base that contains the linked table.
3. Set **Table** to the linked table (e.g., *Organizations*).
4. For **Lookup Field Name**, choose **Airtable Record ID**.
5. For **Value**, reference the record ID from the linked field in your original data (e.g., the first element of the array).
6. Once the lookup succeeds, open the **Cell details** panel on that column and map the name field (or whichever field you need) to a new column.

Alternatively, you can add a **Formula** or **Lookup** field in Airtable itself that returns the linked record's name as plain text, then re-pull that field into Clay.

## Adding more Airtable fields to an existing table

If you've already pulled Airtable records into a Clay table and want to bring in additional Airtable fields — without re-running the import (which would add duplicate rows) — use a **Lookup Record** column to fetch those extra fields by record ID.

**Step 1 — Extract the Airtable Record ID into a column**

When Clay imports Airtable records, each row stores the underlying Airtable Record ID in the source data. To make it usable as a lookup key:

1. Click on any cell in your Airtable source column (labeled **Rows from: …**) to open the **Cell details** panel.
2. Expand the record entry and locate the **id** field (a string like `recXXXXXXXXXXXXXX`).
3. Hover that field and click **Add to column** to create a new column containing the Record ID. Give it a descriptive name such as *Airtable Record ID*.

**Step 2 — Add a Lookup Record enrichment column**

1. Click **+ Add column** and select **Airtable › Lookup Record**.
2. Set **Base ID** to the same Airtable base your original source uses.
3. Set **Table ID** to the same Airtable table.
4. For **Lookup Field Name**, choose **Airtable Record ID**.
5. For **Lookup Value**, reference the Airtable Record ID column you created in Step 1.
6. Click **Submit** and run the column — each row should show **✅ 1 Record Found**.

**Step 3 — Map the fields you need into new columns**

Click any **1 Record Found** result to open **Cell details**. All Airtable fields for that record are listed. Hover the field you want and click **Add to column** to create a new Clay column from it. Repeat for any additional fields you need.

Once you've extracted all the fields you need, you can delete the Lookup Record column if you no longer need it.
