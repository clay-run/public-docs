---
title: Audiences
description: "Clay Audiences is available on all plans. Free and Trial workspaces get records and segments (up to 1,000,000 records). Launch and legacy Starter/Explorer plans add CSV, people/company search, and Clay table imports. Growth and Enterprise (and legacy Pro) add CRM and data warehouse syncs, with limits of 250,000 and 25,000,000 records respectively."
last_synced: 2026-08-20T01:53:27.941Z
---

# Audiences

**Plan availability:** Clay Audiences is available on **all plans** (including Free and Trial, as of September 2026). What's included varies by tier:

-   **Free** — records and segments, up to 1,000,000 workspace records. Import via CSV, people/company search, and Clay table sends. No CRM or data warehouse integration syncs.
-   **Trial** — same as Free, plus Audiences Sequencer and CLI/MCP audience tools.
-   **Launch** and legacy **Starter/Explorer** — same import options as Free and Trial. Legacy Starter/Explorer workspaces receive Launch-tier Audiences access. No CRM or data warehouse integration syncs.
-   **Growth** and legacy **Pro** — full Audiences, including CRM (Salesforce, HubSpot) and data warehouse (Snowflake, BigQuery) syncs, up to 250,000 CRM/DWH records. Legacy Pro workspaces receive Growth-tier Audiences access.
-   **Enterprise** (including legacy Enterprise) — full Audiences with CRM and data warehouse syncs, up to 25,000,000 CRM/DWH records. Incremental CRM syncs run every 15 minutes (vs. daily on Growth).

Only imported Account, Contact, and Lead records count toward CRM/DWH record limits — Activities (Salesforce Tasks and Events) and Opportunities associated with those accounts do not count toward the record limit.

Clay Audiences is the unified data layer for your workspace.  It combines your CRM, data warehouse, and third-party enrichments into one persistent profile per contact and account, updated in real time.

Use it to build dynamic segments across millions of records, run automated enrichment and signal workflows at scale, and sync results back to Salesforce without managing dozens of separate tables.

Setting up Audiences is four major steps:

1.  **Import your data** — connect Salesforce, HubSpot, Snowflake, or Google BigQuery and bring your records into Audiences.
2.  **Create audiences** — build dynamic segments using filters to target the right contacts and accounts.
3.  **Enrich and monitor** — run bulk enrichments and signals that write data permanently back to each record.
4.  **Write back to your CRM** — sync enriched data and segment membership back to Salesforce.

## Roles and permissions

Viewing and filtering audience data is available to all workspace roles. Most write operations require workspace **Admin** access. The table below shows the full breakdown:

| Action | Admin | Editor | Viewer |
|---|---|---|---|
| View, browse, and filter audience data | ✓ | — | — |
| Create and edit audience segments | ✓ | — | — |
| Run bulk enrichments | ✓ | — | — |
| Add or configure data sources | ✓ | — | — |
| Export individual records to Salesforce | ✓ | — | — |
| Upsert or update records from a Clay table into Audiences | ✓ | — | — |

To change someone’s role, go to **Settings** → **Team** and use the dropdown next to their name. Changes apply immediately. Editors and Viewers who need to create segments, run bulk enrichments, or manage data sources should have their role upgraded to Admin, or ask a workspace Admin to perform those actions on their behalf.