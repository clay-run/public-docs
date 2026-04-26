---
title: Attio integration
source_url: https://university.clay.com/docs/attio-integration
last_synced: 2026-04-26T01:39:41.295Z
upstream_hash: 45834b50b195e796f17a6192b2ad1eb1e969632d6fa30603794c07899d2ec9f1
---

# Attio integration

Pull your Attio records directly into a table as a source and push enriched data back by creating, updating, or upserting records across any Attio object.

Attio is a modern, data-driven CRM built for high-growth teams. Within Clay, you can pull your Attio records directly into a table as a source and push enriched data back by creating, updating, or upserting records across any Attio object. Common workflows include:

-   **Inbound enrichment:** Connect lead sources to Clay, enrich across 150+ data providers, and push complete records to Attio with scoring and routing.
-   **Outbound prospecting:** Build lists in Clay or import Attio records, enrich with company data and intent signals, and push back as qualified deals.
-   **CRM maintenance:** Schedule automatic refreshes to keep records current with job changes, funding rounds, and company updates.

## Creating a table with Attio

1.  In a workbook, click `+ Add` at the bottom.
2.  Search for `Attio` and select from the results.
3.  In the modal, you will be asked to `Select Attio account`.
    -   If you haven't already connected your Attio account, click `+ Add account` and authorize Clay to access your Attio workspace via OAuth.
    -   **_Note:_** _Only Attio workspace admins can authorize this connection._
4.  Select a source and configure its inputs.

### `Source` Import records

Imports records from an Attio object into your Clay table.

**Inputs:**

-   `Object`: The Attio object to import records from (e.g., People, Companies). Populated dynamically from your connected account.
-   `View (optional)`: A saved view in Attio to filter the records by. Populated dynamically from your connected account. If provided, takes precedence over the custom `Filter` query. If neither are provided, all records are returned.
-   `Filter (optional)`: A JSON filter query to narrow which records are imported. See [**Attio's filtering and sorting docs**](https://docs.attio.com/rest-api/guides/filtering-and-sorting) for syntax. Ignored if a `View` is selected.
-   `Sort (optional)`: A JSON sort query to order the imported records. See [**Attio's filtering and sorting docs**](https://docs.attio.com/rest-api/guides/filtering-and-sorting) for syntax.
-   `Limit (optional)`: The maximum number of records to import. The maximum is 50,000 records.

### `Source` Import records from list

Imports records from a specific Attio list into your Clay table.

**Inputs:**

-   `List`: The Attio list to import records from. Populated dynamically from your connected account.
-   `Filter (optional)`: A JSON filter query to narrow which records are imported from the list. See [Attio's filtering and sorting docs](https://docs.attio.com/rest-api/guides/filtering-and-sorting) for syntax.
-   `Sort (optional)`: A JSON sort query to order the imported records. See [Attio's filtering and sorting docs](https://docs.attio.com/rest-api/guides/filtering-and-sorting) for syntax.
-   `Limit (optional)`: The maximum number of records to import. The maximum is 50,000 records.

## Enriching data with Attio

1.  While in a Clay table, click `Add enrichment` and search for `Attio`.
2.  Under `Integrations`, select one of the Attio actions.
3.  In the modal, you will be asked to `Select Attio account`.
    -   If you haven't already connected your Attio account, click `+ Add account` and authorize Clay to access your Attio workspace via OAuth.
    -   **_Note:_** _Only Attio workspace admins can authorize this connection._

### `Action` Create record

Creates a new record in an Attio object. Costs 1 credit per run.

**Inputs:**

-   `Object`: The Attio object to create the record in (e.g., People, Companies). Populated dynamically from your connected account.
-   `Object Schema (optional)`: Attribute fields for the record, populated dynamically based on the selected object. Use these to set values on the new record.

**Outputs:**

-   `Record`: The newly created Attio record.

### `Action` Lookup records

Looks up existing records in an Attio object. Returns up to 10 matching records.

**Inputs:**

-   `Object`: The Attio object to search for records in. Populated dynamically from your connected account.
-   `Record ID (optional)`: The UUID of the record to look up. (Required if no Object Schema attribute filters are provided.)
-   `Object Schema (optional)`: Attribute fields to filter records by, populated dynamically based on the selected object. (Required if Record ID is not provided.)
-   `Extract data by field paths (optional)`: JSON path filters to extract or remove specific fields from the response.

**Outputs:**

-   `Records`: An array of up to 10 matching Attio records.

### `Action` Update record

Updates an existing record in an Attio object by its Record ID. Costs 1 credit per run.

**Inputs:**

-   `Multiselect Behavior`: How to handle multiselect attribute values when updating — either `Append multiselect values` (adds to existing values) or `Overwrite multiselect values` (replaces existing values).
-   `Object`: The Attio object containing the record to update. Populated dynamically from your connected account.
-   `Record ID`: The UUID of the record to update.
-   `Object Schema (optional)`: Attribute fields to update, populated dynamically based on the selected object.

**Outputs:**

-   `Record`: The updated Attio record.

### `Action` Upsert record

Creates a new record or updates an existing one in an Attio object, matched on a unique attribute. Costs 1 credit per run.

**Inputs:**

-   `Object`: The Attio object to upsert the record in. Populated dynamically from your connected account.
-   `Matching Attribute`: The unique attribute to use when determining whether to create or update a record (e.g., email address, domain). Populated dynamically from the writable, unique attributes on the selected object.
-   `Object Schema (optional)`: Attribute fields for the record, populated dynamically based on the selected object.

**Outputs:**

-   `Record`: The created or updated Attio record.

### Run settings

-   **Auto-update:** Recommended when you want new rows added to your Clay table to automatically sync back to Attio.
-   **Only run if:** The enrichment will only run when specified conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/guide/conditional-formulas))

## Best practices

-   **Start with lookup:** Use the free `Lookup records` action first to check for duplicates before creating new records.
-   **Use upsert when uncertain:** If you're unsure whether a record already exists in Attio, use `Upsert record` instead of `Create record` to avoid duplicates.
-   **Enable auto-update for syncing:** Turn on auto-update when you want new rows added to your Clay table to automatically sync back to Attio.
-   **Use conditional runs:** Apply conditional formulas to control when records sync back to Attio based on data quality, enrichment status, or other criteria.

## FAQs

### What Attio objects can I use with Clay?

Any standard or custom object in your Attio workspace is supported. The `Object` dropdown is populated dynamically from your connected Attio account, so all available objects will appear automatically.

### What is the difference between Upsert record and Update record?

`Update record` requires a specific Record ID and always modifies an existing record. `Upsert record` matches on a unique attribute (e.g., email address or domain) and will update a record if a match is found, or create a new one if not. Use Upsert when you're unsure whether a record already exists in Attio.

### What is the difference between the View and Filter inputs?

`View` lets you select a saved view from your Attio workspace, which applies any filters and segments already configured in that view. `Filter` accepts a raw JSON filter query for custom filtering logic. If both are provided, the `View` takes precedence and the `Filter` is ignored.
