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

**Why do some rows show "Run condition not met" on provider or validation columns?**

This is expected when the waterfall is working correctly. "Run condition not met" on a subset of rows — not all rows — means the waterfall's built-in logic skipped that step for those rows:

- **An earlier provider already found a valid number for that row.** The Mobile Phone waterfall runs providers in sequence and stops as soon as one returns a result (or a validated result, if validation is enabled). Once an earlier provider succeeds for a row, all subsequent provider columns are skipped for that row — they show "Run condition not met" because the built-in condition "only run if no valid number has been found yet" is no longer true. This is the waterfall stopping early as intended, saving credits by not running additional providers once a match is found.

- **The corresponding provider returned no number, so the validation step was skipped.** Each validation column runs only when the provider step before it returned a phone number. If a provider found nothing for a row, the paired validation column shows "Run condition not met" — there is no number to check. No credits are charged for skipped validation steps.

In both cases, "Run condition not met" on some rows is not an error — it means the waterfall is operating as designed.

**If all rows on every provider step show "Run condition not met"**, that indicates a run condition set on the waterfall column itself or on each provider step is blocking all rows from running. This is different from normal per-row skipping. To diagnose: click into one of the affected cells and use the **Explain** button next to the "Run condition not met" status to see why the condition evaluated to false for that row, then review and adjust the **Only run if** condition on the waterfall column or that provider step. See [Conditional runs](conditional-runs.md) for how run conditions work.

**What match rate should I expect?**

Individual phone providers typically cover only 20–40% of contacts — that low per-provider rate is why the waterfall exists. By stacking providers in sequence, each one checking contacts that previous providers missed, overall coverage rises substantially above what any single provider achieves.

Match rates vary based on:

- **Input data quality** — providing a LinkedIn or personal profile URL is the single strongest input; rows with only a name and company domain will have lower match rates.
- **Your list composition** — coverage differs by geography, industry, and contact seniority. Select the regional waterfall option that matches where your contacts are based (for example, `US & Canada Mobile Phone` or `Europe Mobile Phones`).
- **Number of providers** — a longer provider sequence gives more opportunities to find a number that earlier providers missed. If your current match rate is low and input data is populated, try expanding the waterfall sequence by adding more providers.

If you're seeing unexpectedly low results after providing strong input data and using multiple providers, switch from `Mobile Phone (Global)` to a region-specific option if most of your contacts are in one geography.
