---
title: Clay Ads compliance best practices
description: Explains Clay Ads' automatic targeting controls for US and international audiences, including how Clay-sourced data is handled for Google Ads compliance.
last_synced: 2026-08-24T17:01:32.385Z
---

# Clay Ads compliance best practices

Understand which ad platforms require first-party data and how Clay filters audiences to meet their requirements.

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
-   **Google and Bing, any region:** Your first-party data ✅, Clay-sourced data ❌

### Why this distinction exists

Many regions outside the US, most notably the EU under GDPR, require explicit, opt-in consent before someone can be targeted with ads. That consent lives in your own systems, which is why non-US audiences must be built from your first-party data rather than from Clay's dataset. Sourcing US-based audiences from Clay's data is supported because the US doesn't operate under the same opt-in framework.

## Platforms that require first-party data

Google and Bing don't allow advertisers to use third-party sourced data when building audiences on their platforms, and Clay enforces this for both. This rule is stricter than the regional rules above: a contact sourced from Clay's data is ineligible for Google and Bing no matter where that contact is located, so the US allowance doesn't apply.

What you'll see depends on where you set the sync up.

### Setting up a sync from an audience segment

In the `Select ad providers` modal, `Google Ads` and `Bing Ads` are both marked `For use with first-party data only.` You can still select them. Clay then evaluates every contact in the segment individually and syncs only the ones backed by first-party data, leaving the rest out.

Clay tells you how many contacts this affects before anything syncs. When you create the sync, a confirmation step titled `Creating an ad sync will remove [number] contacts` lists the reasons that apply to your selection. Once the sync exists, the audience header shows a yellow badge reading `Ad syncs exclude [number] people sourced from Clay`.

### Setting up a sync from a workbook table

On this path the check is all-or-nothing rather than per-contact. If any field in the table was populated by a Clay source, `Google Ads` is disabled entirely for that audience and shows a `First-party only` badge with the message `Google Ads only supports contacts sourced from first-party data.` There's no partial sync to fall back on — to advertise on Google, build the audience in a table whose fields all come from your own data.

`Bing Ads` is only offered as a destination for audience segments, so you won't encounter it on this path.

**Note:** Clay counts a contact as Clay-sourced only when Clay's data is that contact's sole source. A contact you imported from your CRM, data warehouse, or a CSV keeps its first-party status even after you enrich it with Clay — so enriching your own records doesn't make them ineligible for Google or Bing. That covers the enrichments most ad audiences rely on, including additional emails and `Enhanced matching` results.

## How Clay-sourced contacts are filtered for other platforms

For destinations other than Google and Bing — such as `Meta Ads` — contacts sourced from Clay's data are eligible, but only where the regional rules allow it. Clay checks each contact's country and includes a Clay-sourced contact when that country is the US, or when the country is blank because Clay doesn't have it. Clay-sourced contacts with any other country are left out of the sync.

The badge on the audience header names this case specifically: `Ad syncs exclude [number] people sourced from Clay outside the US`.

Because Clay applies this contact by contact, a segment that mixes US and non-US people still syncs — just with fewer contacts than the segment's total. Contacts that came from your own first-party data are never filtered on country.

## Restricting Clay data in Ad Sync tables

Rather than relying on filtering at sync time, you can stop non-compliant audiences from being built at all. Under `Ads settings`, the `Restrict Table Ad Sync enrichments` control has a `First-party only` toggle, described as `When enabled, only your CRM and Warehouse data are available in Table Ad Syncs`. With it on, Clay's enrichment providers no longer appear as options inside Ad Sync tables.

## Best practices

-   **Collect and store consent in your own systems.** For non-US audiences especially, build from first-party data (CSV, CRM or data warehouse) where consent has been captured.
-   **Plan Google and Bing campaigns around first-party data.** Clay-sourced contacts never reach either platform, in any region, so build those audiences from your CRM, data warehouse, or CSV data. Read the excluded-contact count on the confirmation step before you create the sync so your delivered audience size isn't a surprise.
-   **Fill in country data on contacts you own.** For platforms other than Google and Bing, a Clay-sourced contact with a country outside the US is dropped, while a blank country is allowed through. If you hold reliable country data in your own systems, sync it into Audiences so eligibility is decided on real values rather than gaps.
-   **Keep opt-outs current in your source systems.** We recommend you sync opt-out status into Audiences and filter out these users from your Ad Sync segments. Recurring syncs run every 3 days, so removing someone in your source will flow through to your connected ad account on the next sync cycle.
-   **Build net-new reach from a seed list you own.** Create a lookalike audience from a customer list sourced from your own systems, then exclude that seed list in the campaign so spend goes to people you haven't reached yet. Because the seed is first-party, it's eligible on every destination, Google and Bing included.
-   **Check what your own terms already cover.** If your terms of service or privacy notice tell customers their data may be used for advertising, that gives you a clear basis for targeting them. Worth confirming with whoever owns that language before you build the audience.

## Frequently asked questions

**Can I use Clay's data to build a non-US ad audience?**  
No. Clay's dataset can't be used to source people outside the US for ad targeting. Use your own first-party data for non-US audiences.

**Can I use Clay's data to build a US ad audience?**  
Yes. You can use Clay's data to source and build audiences of US-based people.

**Do these rules apply to an audience I only use for exclusion?**  
Yes. Clay applies the sourcing and country filters when it builds the audience, and whether you attach it as targeting or as an exclusion is chosen later in the ad platform's campaign manager. So a suppression list is filtered on exactly the same basis as a targeting list. If you need every contact on the list to land, build it from your own data.

**Do these sourcing and country rules apply to company audiences?**  
No. Clay applies them to contact audiences only. Company audiences aren't filtered on how their data was sourced or on country.

**Who can change the workspace ads settings that restrict Clay data?**  
Only workspace admins. The `First-party only` toggle under `Ads settings` is visible to everyone but editable only by admins.

**My segment and my synced audience show different counts. Is something broken?**  
No. The segment count is everyone matching your filters, while the synced count is only the contacts eligible for the destinations you picked. The difference is the excluded contacts, and the badge on the audience header tells you which rule accounts for them.

**How quickly do opt-outs take effect?**  
Recurring syncs run every 3 days. Opt-outs updated in your source system are reflected in your connected ad account on the next sync cycle.

**Which fields are hashed before they reach an ad platform?**  
This varies by destination, since each platform sets its own specification and Clay follows it. Google Ads takes email, phone, first name, and last name as SHA-256 hashes, while country and zip code are sent unhashed to match Google's specification. Meta Ads hashes every field Clay sends it, country and zip code included. LinkedIn Ads and Bing Ads hash the email address and send the remaining fields as plain text.
