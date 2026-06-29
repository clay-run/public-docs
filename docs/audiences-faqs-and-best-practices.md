---
title: Audiences FAQs and best practices
description: Frequently asked questions and best practices for using Clay Audiences, covering when to use Audiences vs. tables, CRM setup, enrichments, and segment building.
last_synced: 2026-06-23T13:49:47.033Z
---

# Audiences FAQs and best practices

Common questions and best practices for using Clay Audiences.

Clay Audiences is the unified data layer in Clay — one always-current home for all your sales data that enriches itself, keeps your lists live, and turns signals into actions. This page covers best practices for getting the most out of Audiences and answers to frequently asked questions about how it works.

## **FAQs**

### When should I use Audiences vs. a table?

Use Audiences by default for anything you want to reuse, segment on, or build automations on top of. Use tables for one-off workflows, integrations Audiences doesn't yet support natively, or cases where data doesn't need to persist beyond a single run.

The simplest framing: Tables are how you _work on_ data. Audiences is where your data _lives_. They work together — you still build and run workflows in Tables, they just pull from a cleaner, richer, always-current foundation.

|  | Clay Tables | Audiences |
| --- | --- | --- |
| Best for | One-off, one-time workflows | "Always-on" workflows that keep running |
| Role | How you work on data | Where your data lives |
| Scope | A specific working set you build and run | A slice across your entire dataset |
| Connections | Built per workflow | Continuously synced to your CRM, warehouse, and other sources |
| Scale | Up to 50,000 rows | Millions of records |

### What if my integration isn't supported yet?

Use the `Upsert Audiences Record` table enrichment as a bridge. Bring your data into a Clay table from any source, then use Upsert to push those records permanently into your Audience. This works for any source Audiences doesn't yet natively support.

### My CRM is messy. Should I clean it up before setting up Audiences?

You don't need a clean CRM to get started — CRM cleanup is often the first use case Audiences enables. A common approach: sync your existing CRM, run professional network enrichments to refresh contact data, use the enriched identifiers to surface duplicates, then build further enrichments from there.

### Does Audiences update automatically?

Yes. Segments update in real time as records enter or exit your filter criteria. The refresh frequency depends on your plan:

-   **Enterprise plan:** CRM and data warehouse syncs run every 15 minutes, and segments update continuously.
-   **Growth plan:** CRM and data warehouse syncs run daily, and segments update based on that daily refresh.

Enrichments configured with `Continuous Enrichment` enabled automatically process new records entering a segment, typically within 15 minutes.

### **How does Clay handle Salesforce Lead-to-Contact conversions?**

When a Salesforce Lead is converted into a Contact in Salesforce, Clay automatically merges the Lead record with the Contact record in Audiences. The data from both records is combined into a single person record, and all historical data is preserved. This merging happens automatically and is not user-configurable.

### **What's the difference between automatic Lead/Contact merging and deterministic matching?**

There are two types of record matching in Clay Audiences:

-   **Automatic Lead/Contact merging** — When Salesforce converts a Lead to a Contact, Clay automatically merges these records. This is Salesforce-specific and not user-configurable.
-   **Deterministic matching** — User-configurable matching across different data sources. You choose which field to match on (email, domain, profile URL, etc.) when importing a new source. This allows you to merge the same person or company across Salesforce, Snowflake, HubSpot, and other sources.

Both work together to ensure you have a single, unified record per person or company in your Audiences.

## **Best practices**

### **Start with RevOps, not marketing or sales**

The fastest path to a working setup runs through whoever owns the CRM keys — typically a RevOps lead or manager. Starting with another team means going back to RevOps for CRM authorization, which can take days. Starting with RevOps means a live CRM sync in under 20 minutes.

### **Import before you export**

Turn on import first, validate Clay's data quality, then enable write-back once you trust what you're seeing.

### **Import more fields than you think you need**

You can hide fields you don't use, but adding fields not imported at setup requires reconfiguring your sync. Fields that weren't imported can't be used as segment filters. When in doubt, include it.

### **Filter before enriching**

Define your audience filters before running Bulk Enrich. Credits are charged per record enriched — if you enrich `All People` instead of a filtered segment, you pay for every record in your database. The narrower your audience, the more targeted and cost-efficient your enrichment run.

### **Test enrichments on 10 rows before running at scale**

Before running across your full segment, click `Run on 10 rows` and confirm the output is correct and field mapping is configured as intended. Given the credit implications of a misconfigured enrichment across millions of records, treat this as a standard step every time.

### **Check your field mapping intent before hitting `Start Run`**

Field mapping is on by default. If you want enriched data to write back to Audiences, confirm your column mappings are configured. If you're running an enrichment purely to trigger an action without saving data, explicitly disable field mapping so the run behaves as expected.

### **Work backwards from the use case when building segments**

Don't start with the data and ask what to filter. Start with the finish line: what action will be taken on this segment, and by whom? Segment by rep assignment for outbound, by product signals for PLG, by deal stage for pipeline plays.

### **Use CPJ draft mode to qualify records before committing**

Records from People Search land in draft state before entering `All People`. Use this window to apply additional filters, run a quick enrichment, and verify quality before clicking `Commit` — credits for downstream enrichments and actions are not spent until records are live.

### **Schedule large initial syncs at end of day**

For enterprise customers where Salesforce is live and operational, start large initial syncs near end of business EST. If the sync generates high load, it won't interfere with critical business functions.

### **Do the API math with nervous admins**

Divide your total record count by 50,000 (import batch size) to estimate import API calls, or by 10,000 for export. For most enterprise customers, the math makes this a non-issue — a 5M-record CRM generates only 100 import API calls against a Salesforce limit typically around 150 million records per day.

### **Start narrow, then expand**

Start with one scoped use case, demonstrate value, then expand. Customers who see one use case working naturally discover the next — signals lead to TAM sourcing, TAM sourcing leads to account matching. Trying to configure everything at once often stalls progress.
