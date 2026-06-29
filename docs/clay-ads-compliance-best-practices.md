---
title: Clay Ads compliance best practices
description: Explains Clay Ads' automatic targeting controls for US and international audiences, including how Clay-sourced data is handled for Google Ads compliance.
last_synced: 2026-06-22T15:12:14.779Z
---

# Clay Ads compliance best practices

Keep your ad campaigns compliant with Clay's automatic targeting controls for US/international audiences and Google Ads.

When you build an advertising audience in Clay Ads, Clay automatically applies a set of built-in controls that determine which contacts are eligible for ad targeting based on where they're located and how their data was sourced. These controls run behind the scenes every time you build and sync an audience, so you don't have to manage them manually.

## How audience sourcing works by region

The data you can use to build an ad audience depends on where the people you're targeting are located.

### Ad targeting in the United States

You can use Clay's data to source and build ad audiences of US-based people. This includes audiences built from Clay's enrichment and data providers.

### Ad targeting outside the United States

Today, you're not able to source contacts outside the US for ad targeting. This is a built-in restriction designed to keep your campaigns aligned with stricter consent requirements in regions like the EU.

To target people outside the US, you can use **your own first-party data,** for example, contacts from your CRM or data warehouse where you've collected the appropriate consent.

**Quick summary**

-   **US audiences:** Clay-sourced data ✅ and your first-party data ✅
-   **Non-US audiences:** Your first-party data ✅, Clay-sourced data ❌

### Why this distinction exists

Many regions outside the US, most notably the EU under GDPR, require explicit, opt-in consent before someone can be targeted with ads. That consent lives in your own systems, which is why non-US audiences must be built from your first-party data rather than from Clay's dataset. Sourcing US-based audiences from Clay's data is supported because the US doesn't operate under the same opt-in framework.

## Advertising on Google

Google's advertising policies don't allow advertisers to use third-party sourced data when building audiences on Google's platform.

To keep your Google campaigns compliant, Clay automatically **filters out any Clay-provided data** when syncing an audience to Google. Only your first-party data flows through to your Google Ads account and any contacts or fields that originated from Clay's dataset are removed before the sync.

This happens automatically, so you don't need to manually separate your data sources before syncing to Google.

## Best practices

-   **Collect and store consent in your own systems.** For non-US audiences especially, build from first-party data (CSV, CRM or data warehouse) where consent has been captured.
-   **Use first-party data for Google campaigns.** Since Clay-provided data is filtered out on sync to Google, plan Google audiences around your own data.
-   **Keep opt-outs current in your source systems.** We recommend you sync opt-out status into Audiences and filter out these users from your Ad Sync segments. Clay runs full replacement syncs every 2 days, so removing someone will flow through to your connected ad account on the next sync.

## Frequently asked questions

**Can I use Clay's data to build a non-US ad audience?**  
No. Clay's dataset can't be used to source people outside the US for ad targeting. Use your own first-party data for non-US audiences.

**Can I use Clay's data to build a US ad audience?**  
Yes. You can use Clay's data to source and build audiences of US-based people.

**Why isn't all of my data showing up in my Google audience?**  
When syncing to Google, Clay filters out any data it provided, because Google doesn't allow third-party sourced data on its platform. Your first-party data will sync as expected.

**How quickly do opt-outs take effect?**  
Clay runs full replacement syncs up to every 2 days, so opt-outs updated in your source system are reflected in your connected ad account on the next sync cycle.
