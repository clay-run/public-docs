---
title: Bulk enrichment
source_url: https://university.clay.com/docs/bulk-enrichment
description: Enrich millions of rows quickly, securely, and at scale. No row
  limits, no slowdown.
last_synced: 2026-04-27T18:09:27.586Z
upstream_hash: 85ced5e9b3b33801cc3cc02219f8d58a400adaa1f821746b1b9271988d479f7a
---

# Bulk enrichment

Enrich millions of rows quickly, securely, and at scale. No row limits, no slowdown.

# Bulk enrichment

**Bulk enrichment** makes it easy to process massive datasets—no row limits, no slowdown. Enrich millions of rows quickly, securely, and at scale.

You'll get the full power of Clay's enrichment engine without storing data inside Clay. Results are sent directly to your external destinations, like Salesforce, Snowflake, or Google Sheets, keeping your systems continuously enriched and in sync.

Once your data is successfully exported, enriched rows are automatically deleted to keep your workspace clean and efficient.

## Setting up a bulk enrichment

### Import from CSV

1.  On the homepage, click `New` → `Bulk enrichment`.
2.  Select `Source type` → `Import from CSV`.
3.  Select `Delimiter`.
    -   A delimiter is the character that separates values in your CSV file (e.g., comma, semicolon, or tab).
4.  Click `Save` and start adding [enrichments](https://www.clay.com/university/guide/enrichments) normally.

### Import from CRM (Salesforce)

1.  On the homepage, click `New` → `Bulk enrichment`.
2.  Select `Source type` → `Import from CRM`.
3.  Next, `Select Salesforce account`.
    -   Click `Add account` if you haven't already authenticated your account.
4.  Select inputs from `Salesforce object` and `List view`.
5.  Click `Save` and start adding [enrichments](https://www.clay.com/university/guide/enrichments) normally.

### Using a bulk enrichment

In the bulk enrichment settings, you can adjust several options:

-   `Test data`: Add rows to test your enrichments before running the full source.
-   `Export data`: Set up your export destination.
    -   This could be Salesforce, Google Sheets, Snowflake, etc.
-   `Deletion criteria`: Single column or conditional rules.
    -   You can also `Archive deleted rows` for up to 30 days, meaning they will remain indexed and searchable.
-   `Run starting point`: Decide whether to clear rows already in the test table and rerun them.
