---
title: Salesforce SOQL
source_url: https://university.clay.com/docs/salesforce-soql
description: The Salesforce SOQL source enables you to import records from
  Salesforce by writing custom queries or generating them with AI from a plain-language description.
last_synced: 2026-04-26T01:40:35.632Z
upstream_hash: c8f21c092741d6111a8d95755a222978fedfe8960b7ef0717559be2afaaf3eca
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

-   **SOQL Query:** Your SELECT statement with explicitly listed fields (e.g., `SELECT Id, Name, Industry FROM Account WHERE Industry = 'Technology' LIMIT 100`). Clay can also generate this query for you — see [Generating queries with AI](#generating-queries-with-ai) below.
-   **Unique Fields (Optional):** Select which field(s) determine record uniqueness for deduplication (e.g., `Id`, `Email`).

**Query requirements:**

-   Must be a valid SELECT statement.
-   Fields must be explicitly named (no `SELECT *`).
-   Maximum 50,000 records per import.

**Pro tip:** Keep Salesforce's [**SOQL documentation**](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) open while building queries by hand.

## Generating queries with AI

> **Early access:** AI query generation is currently available to selected workspaces. Contact the Clay team to enable it for your workspace.

Instead of writing SOQL by hand, you can describe the Salesforce data you want in plain language and Clay will generate the query for you. This works in both the **Import records from a Salesforce SOQL query** source and the **Lookup records via SOQL** enrichment action, and supports standard objects as well as custom objects.

**How to use it:**

1.  In the SOQL query input, click **Generate with AI**.
2.  Describe the data you want — for example, "All open opportunities over $50,000 in the Technology industry, including account name and owner."
3.  Click **Generate**. Clay will explore your Salesforce schema and write the query.
4.  Optionally, click **Test query** to run a 1-row preview and confirm the query returns what you expect.
5.  Review any **suggested fields** Clay surfaces — these are related fields on the same object you may also want to include.

**How Clay selects the right fields:**

Clay reads your org's live Salesforce schema — it does not rely on generic Salesforce knowledge and does not require any training or configuration on your part. When you describe what you want, Clay:

1.  Lists all queryable objects in your Salesforce org.
2.  Inspects the field definitions (API names, labels, types, and descriptions) of the relevant object.
3.  Selects the field whose metadata best matches your description.

If your org has several similarly named custom fields, include the field's exact label or API name in your description to help Clay select the right one (e.g., "the `Custom_Revenue__c` field").

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

Yes! Use Clay's auto-update feature to re-run your query on a schedule.

### Why am I getting rate limit errors?

Salesforce enforces API request limits. If you hit limits:

1.  Reduce query frequency
2.  Limit concurrent Salesforce operations
3.  Contact Salesforce support to increase your API allocation

### How does Clay know which custom field I want when several have similar names?

Clay reads your org's live Salesforce schema at generation time, inspecting the API names, labels, types, and descriptions of fields on the object you're querying. If several custom fields have similar names, include the exact field label or API name in your description to help Clay select the correct one.

### Do I need to train the AI or configure anything before using AI query generation?

No training or data setup is required. The AI reads your org's schema directly each time you generate a query. AI query generation is currently an early-access feature — contact the Clay team to enable it for your workspace.
