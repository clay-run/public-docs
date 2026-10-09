---
title: Salesforce SOQL
description: The Salesforce SOQL source enables you to import records from
  Salesforce by writing custom queries.
last_synced: 2026-04-26T01:40:35.632Z
---

# Salesforce SOQL

The Salesforce SOQL source enables you to import records from Salesforce by writing custom queries.

The Salesforce SOQL source enables you to import records from Salesforce by writing custom queries, giving you complete control over which data to pull into Clay.

Use this when you need specific Salesforce records that don't match an existing list or report, want to query across related objects, or need complex filtering that's easier to express in SOQL.

## Creating a table with Salesforce SOQL

1.  In a workbook, click `+ Add` at the bottom.
2.  Search for `Salesforce SOQL` and select from the results.
3.  In the modal, you will be asked to `Select Salesforce account`.
    -   If you haven't already connected your Salesforce account, click `+ Add account` and go through authentication.

### `Source` Import records from a Salesforce SOQL query

Build lists of Salesforce records using custom SOQL queries. Query across objects, apply complex filters, and select specific fields without creating dedicated lists in Salesforce first.

**Inputs:**

-   **SOQL Query:** Your SELECT statement with explicitly listed fields (e.g., `SELECT Id, Name, Industry FROM Account WHERE Industry = 'Technology' LIMIT 100`).
-   **Uniqueness fields (Optional):** Select one or more fields that together uniquely identify each record. Clay hashes the values of all selected fields to form a composite key, which it uses to skip duplicate rows during import and re-syncs.

    You can select **multiple fields** to create a compound key. For example, if you're importing Opportunities with Contact Roles — where the same contact can appear multiple times with different roles — select `OpportunityId`, `ContactId`, and `Role` together. Clay treats each unique combination as a distinct row, preserving all contact-role pairs.

    If no fields are selected, Clay uses the entire row content as the unique identifier, which can cause duplicate rows when individual field values change across syncs.

**Query requirements:**

-   Must be a valid SELECT statement.
-   Fields must be explicitly named (no `SELECT *`).
-   Maximum 50,000 records per import.

**Pro tip:** Keep Salesforce's [**SOQL documentation**](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) open while building queries. You can also use AI tools like Claude or ChatGPT to help generate SOQL queries from natural language descriptions.

## Workflow: enrich Salesforce records and write them back on a schedule

A common pattern with the SOQL source is to import a filtered set of Salesforce records, enrich them with Clay data providers, and write the enriched data back to Salesforce automatically on a recurring schedule. For example: import all Leads with no email address, find their work emails using Clay enrichments, then push those emails back onto the Lead record in Salesforce weekly.

**Step 1: Build your SOQL query**

Write a query that selects only the records needing enrichment — and all the fields your enrichments will use as inputs. For example, to target Leads with no email address:

```sql
SELECT Id, FirstName, LastName, Company, Title
FROM Lead
WHERE Email = null
LIMIT 50000
```

Include every field an enrichment will read as an input. If an email-finding provider needs a company domain and your Leads don't have one, include `Website` in the `SELECT` clause so it's available in your table.

**Step 2: Schedule the source**

In the source settings, set **Run this source** to **On a schedule** and choose a frequency. To run weekly, select **Week**. To have Clay refresh the data for records already in your table on each run, enable **Update existing rows**.

See [Scheduled sources](scheduled-sources.md) for all available frequencies and plan limits.

**Step 3: Add enrichment columns**

Add enrichment columns for the data you want to find. For email, a Work Email Waterfall — which tries multiple email-finding providers in sequence — maximizes coverage. If a provider requires a company domain that isn't already in your table, add a company domain enrichment first and use its output as input to the email waterfall.

**Step 4: Write back with Salesforce Update Record**

Add a Salesforce **Update Record** action column. Set **Record ID** to the `Id` column returned by your SOQL source. In **Map fields**, add the fields you want to write back to Salesforce and map them to the enriched columns in your Clay table — for example, map your found email column to the **Email** field on the Lead object.

Add a [conditional run](conditional-runs.md) to the Update Record column so it only fires when enrichment returned a result — for example, when the found email column is not empty. This prevents overwriting existing Salesforce data with blank values on rows where enrichment didn't find anything.

**50,000-record limit**

Each SOQL source run imports a maximum of 50,000 records. If your filtered Lead population could exceed this, add a `WHERE` condition to keep each run under the limit — for example, `AND CreatedDate >= LAST_N_DAYS:90` to process a recent subset. Expand the date range over subsequent runs until all records are covered.

## Best practices

### Start with test queries

Always test queries with a `LIMIT` clause before running them on large datasets:

-   `SELECT Id, Name FROM Account LIMIT 10`

### Query only needed fields

Selecting fewer fields makes queries faster and reduces permission errors:

✅ **Do this:**

-   `SELECT Id, Name, Industry FROM Account`

❌ **Avoid this:**

-   `SELECT Id, Name, Description, CreatedDate, CreatedById, LastModifiedDate, LastModifiedById, ... (20+ fields)`

### Use indexed fields for performance

Salesforce queries run faster when filtering on indexed fields like `Id`, `Name`, `CreatedDate`, and `SystemModstamp`.

### Be mindful of the 50,000 record limit

For larger datasets, break queries into smaller batches using `WHERE` conditions (e.g., by date ranges).

### Respect field-level security

Clay inherits Salesforce permissions from your connected user. If your query includes fields you don't have access to, it will fail with a permission error.

### Querying related objects

Use dot notation to pull data from parent objects:

```javascript
SELECT Id, FirstName, LastName, Account.Name, Account.Industry
FROM Contact
WHERE Account.Type = 'Customer'
```

## FAQs

### What Salesforce permissions do I need?

Your Salesforce user must have:

-   **View access** to objects and fields in your query
-   **API Enabled** permission
-   OAuth scopes: `api`, `refresh_token`, `id`, `profile`

### Why is my query failing with a "field not found" error?

Common causes:

1.  Typo in field name (case-sensitive)
2.  Field doesn't exist on that object
3.  Custom fields missing `__c` suffix (e.g., `MyCustomField__c`)
4.  Insufficient permissions

**Troubleshooting tip:** Test your query in Salesforce's Developer Console (Setup → Developer Console → Query Editor) to isolate whether the issue is with the query or Clay's connection.

### Can I use SOQL functions like COUNT() or aggregate queries?

Not currently. Clay's SOQL source only supports standard SELECT queries that return records.

**Workaround:** Import raw records and use Clay's formula columns to perform calculations.

### What happens if my query returns more than 50,000 records?

Clay will import the first 50,000 records and stop. Split your query using date ranges or filters to work with larger datasets.

### How do I query custom objects?

Use the API name with the `__c` suffix:

```javascript
SELECT Id, Name, Custom_Field__c
FROM Custom_Object__c
WHERE Status__c = 'Active'
```

### Can I schedule SOQL queries to run automatically?

Yes. In your source settings, set **Run this source** to **On a schedule** and choose a frequency — hourly (Enterprise only), or daily, weekly, monthly, quarterly, or custom (all plans). Enable **Update existing rows** to have Clay refresh the data for any record returned by each run.

**Important:** Only records returned by the SOQL query during a given run are created or updated. If a record is not returned — for example, because it no longer satisfies your `WHERE` clause — it will not be updated, and the row in your Clay table will retain its previous values. See below for details.

### If I update my SOQL query to add new fields, will existing rows get those fields?

Not by default. When you update your SOQL query to add fields to the SELECT clause, Clay will only bring in net-new records — those not already matched by your configured **Uniqueness fields**. Existing rows won't be updated with the new field data.

To populate the new field on existing rows, you have two options:

-   **Enable "Update existing rows"** in your source settings. When this toggle is on, the next source run re-imports all records returned by the query — including existing rows — and populates them with the latest field data. Find this toggle in the source column settings or the schedule configuration.
-   **Add a Salesforce Lookup record enrichment column** targeting the specific field you want. This fetches only that field for each existing row without re-running the full import, giving you more surgical control over which rows get updated.

### Why aren't my existing rows being updated even though "Update existing rows" is on?

The most common cause is that the record is no longer returned by your SOQL query. **"Update existing rows" only applies to records that the query actually returns during each run** — it does not re-process all rows already in your table.

Think of each scheduled run as Clay asking Salesforce: "Give me all records matching `{your query}`." If Salesforce doesn't return a particular record, Clay has no way to know it needs updating.

**To diagnose:** Run your query directly in Salesforce's Developer Console (Setup → Developer Console → Query Editor). If the record you expect to update does not appear there, it will not be updated in Clay.

**To fix:** Rewrite your query so it returns the records you want to keep current. Common approaches:

-   Remove or broaden the `WHERE` condition that may now exclude the record (e.g., if you're filtering on a field that changed value).
-   Add a condition to catch recently modified records: `WHERE ... OR SystemModstamp >= LAST_N_DAYS:30`.
-   If you need to track a fixed set of accounts regardless of their field values, filter on a stable identifier instead (e.g., `WHERE Id IN ('001...', '001...')`).

### Why am I getting rate limit errors?

Salesforce enforces API request limits. If you hit limits:

1.  Reduce query frequency
2.  Limit concurrent Salesforce operations
3.  Contact Salesforce support to increase your API allocation
