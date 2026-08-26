---
title: Mobile Phone waterfall
description: Find mobile phone numbers faster — the Mobile Phone waterfall
  cascades across multiple providers in sequence, stopping as soon as a result
  is found.
last_synced: 2026-07-22T18:46:10.000Z
---

# Mobile Phone waterfall

Find mobile phone numbers faster — the Mobile Phone waterfall cascades across multiple providers in sequence, stopping as soon as a result is found.

The Mobile Phone waterfall finds a person's mobile (cell) phone number by querying phone data providers one at a time, in a set order. Instead of relying on a single provider — which typically covers only ~20–40% of contacts — the waterfall stacks providers to push coverage substantially higher.

You only pay credits for the provider that finds a match, making it one of the most credit-efficient ways to build phone coverage at scale.

**Available on:** Launch plan or higher. Phone number enrichments are not available on free or trial plans — this restriction applies even if you have unused data credits. To access the Mobile Phone waterfall, upgrade to a paid plan. See [Plans & billing](plans-and-billing.md#trials) for details.

## Setting up the Mobile Phone waterfall

1.  In your table, click `Add enrichment` in the top right corner.
2.  Search for `Mobile Phone` and select it from the results.
3.  Choose between `Quick setup` and `Full configuration`.
4.  Map your input columns and click `Save`.

The `Validation` advanced setting is available in `Full configuration` mode.

### Inputs

The stronger the identifiers you provide, the higher your hit rate:

- **LinkedIn / personal social profile URL** — the single most accurate input; include it whenever available.
- **Full Name + Company Domain** (or company name) — a solid fallback when no profile URL is available.
- **Work Email** — can also be used to match a contact to a mobile number.

Map whichever of these columns you have. Providing more than one identifier improves match rates.

### How it works

Once the enrichment starts, Clay moves through the waterfall dynamically. If a provider returns a mobile number, the process stops for that contact and (where applicable) the results of unused providers are not charged. If a provider returns nothing, Clay moves on to the next provider until a number is found or all providers are exhausted.

## Optimize for (location)

The `Optimized For` setting controls which version of the waterfall runs. You can base your choice on the inputs you have or on the outcome you want. By default, Clay selects `Mobile Phone (Global)` — the most universal version of the waterfall. To target a specific region, open the dropdown and choose the option that best matches where your contacts are based.

- `Mobile Phone (Global)` *(default)* — the most universal coverage.
- `US & Canada Mobile Phone`
- `Europe Mobile Phones`
- `APAC Mobile Phone`
- `LATAM Mobile Phone`
- `Middle East & Africa Mobile Phone`
- `Mobile Phone (Every Provider)` — runs across the full provider set.

Choosing a region-specific version prioritizes the providers with the strongest coverage for that geography, which can improve match rates and reduce spend when you know where your contacts are located. Your choice here also determines which validators are available (see below).

## Validation

Validation lets you verify each phone number before the waterfall accepts it, so you stop only on numbers that meet your quality bar — not just the first number any provider returns.

**ClearoutPhone** is available for every optimization option. To use it, connect your own **ClearoutPhone API key** — validation cannot run until this key is connected. Once connected, ClearoutPhone checks each candidate number and reports whether it is valid and what line type it is.

**Trestle** is available as a second validator **only** when you've optimized for one of the region-specific waterfalls — `APAC Mobile Phone`, `LATAM Mobile Phone`, `Middle East & Africa Mobile Phone`, or `US & Canada Mobile Phone`. It is not offered for `Mobile Phone (Global)`, `Europe Mobile Phones`, or `Mobile Phone (Every Provider)`. You can run Trestle using either **Clay credits** or your own **Trestle API key**.

Whichever validator you use, two options control how validation behaves:

### Only validate mobile phone types?

By default, the validator returns **all phone line types — including landline and VoIP — as valid**. Enable this setting to consider **only mobile/cellular numbers as valid**; with it on, non-mobile line types will not pass validation, so the waterfall keeps mobile numbers only.

- **Enable** when you strictly need personal mobile numbers — for example, for SMS campaigns or dialing personal cells.
- **Leave off** to accept any valid phone line type.

### Require validation success?

When enabled, the waterfall **only accepts a number that the validator explicitly confirms as valid**. If validation fails or is inconclusive, the number is rejected and the waterfall moves on to the next provider.

- **Enable** for the highest-quality output. This is stricter, so it may call more providers per contact and can lower your overall fill rate.
- **Disable** to have the waterfall accept a provider's number even when validation doesn't succeed. In this mode, validation acts as informational metadata rather than a gate that blocks results.

**Tip:** Enabling both options gives you the strictest result — only validated mobile numbers are kept. Loosening either option trades quality for higher coverage and lower credit spend.

## Additional column settings

These optional settings control how results and intermediate data appear in your table:

- **Output name of successful provider?** — When enabled, adds a column showing which provider returned the accepted number, so you can see source attribution per row.
- **Hide provider columns?** *(enabled by default)* — Hides the intermediate per-provider columns the waterfall uses internally, keeping your table clean. Disable this if you want to inspect the raw output of each provider.

## FAQs

**Do I have to use validation?**
No. Validation is optional. Without it, the waterfall accepts the first number any provider returns. Connecting a validator is recommended when number quality and line type matter.

**Which validators can I use, and do I need my own API key?**
ClearoutPhone is available for every optimization option and runs on your own ClearoutPhone account — connect your API key to enable it. Trestle is available as a second validator only for the region-specific waterfalls (APAC, LATAM, Middle East & Africa, and US & Canada Mobile Phone) and can be run with either Clay credits or your own Trestle API key.

**What's the difference between the two validation options?**
`Only validate mobile phone types?` filters by *line type* — enable it so only mobile/cellular numbers count as valid (by default, all line types, including landline, are considered valid). `Require validation success?` gates by *validation outcome* — keep only numbers the validator confirms valid. You can use them independently or together.

**Will stricter validation cost more credits?**
It can. Rejecting more numbers means the waterfall calls more providers per contact before it finds an acceptable result, which can increase spend and reduce fill rate — in exchange for higher-quality output.

**Some of the phone numbers the waterfall is returning are wrong or outdated — how do I find out which provider is responsible?**
Enable **Output name of successful provider?** in your waterfall's **Additional column settings**. This adds a column to your table showing which provider returned the accepted number for each row. When reps flag a bad number, check that column to identify a pattern — if the same provider appears repeatedly on flagged rows, that provider may have stale data for your specific audience or geography.

To compare providers directly before committing to a waterfall order, run individual provider enrichments on the same set of contacts rather than nesting waterfalls. Running them as separate columns makes each provider's result visible and attributable, so you can evaluate accuracy across sources side by side. Once you've identified which providers consistently return the most accurate results for your use case, reorder or disable underperformers in the waterfall's **Waterfall sequence** configuration.
