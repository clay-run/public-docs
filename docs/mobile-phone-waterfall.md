---
title: Mobile Phone waterfall
description: Find mobile phone numbers faster — the Mobile Phone waterfall
  cascades across multiple providers in sequence, stopping as soon as a result
  is found. Also explains how to find a work (corporate) direct-dial number.
last_synced: 2026-07-22T18:46:10.000Z
---

# Mobile Phone waterfall

Find mobile phone numbers faster — the Mobile Phone waterfall cascades across multiple providers in sequence, stopping as soon as a result is found.

The Mobile Phone waterfall finds a person's mobile (cell) phone number by querying phone data providers one at a time, in a set order. Instead of relying on a single provider — which typically covers only ~20–40% of contacts — the waterfall stacks providers to push coverage substantially higher.

You only pay credits for the provider that finds a match, making it one of the most credit-efficient ways to build phone coverage at scale.

**Plan availability:** The Mobile Phone waterfall requires the **Launch plan or above**. It is not available on the Free plan or during the free trial period — this restriction applies even if you have unused data credits. Work email enrichment, people search (Find People), and LinkedIn profile resolution (Enrich Person) work on all plans including Trial — so you can build and validate the rest of your table workflow before upgrading. To upgrade, go to **Settings → Plan & billing**. See [Plans & billing](plans-and-billing.md#trials) for details.

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

## Editing the Mobile Phone waterfall

To change the region, adjust validation settings, or add, remove, or reorder providers in a Mobile Phone waterfall you've already saved:

1.  Click the waterfall tab — the labeled bar spanning your waterfall's provider columns — to open the waterfall menu, then select **Edit group**.
2.  In the waterfall editor, click the **Full configuration** tab.
3.  Make your changes — update **Optimized For**, **Validation**, **Waterfall sequence**, or **Additional column settings** as needed.
4.  Click **Save**.

## Optimize for (location)

The `Optimized For` setting controls which version of the waterfall runs. You can base your choice on the inputs you have or on the outcome you want. By default, Clay selects `Mobile Phone (Global)` — the most universal version of the waterfall. To target a specific region, open the dropdown and choose the option that best matches where your contacts are based.

- `Mobile Phone (Global)` *(default)* — the most universal coverage.
- `US & Canada Mobile Phone`
- `Europe Mobile Phones`
- `APAC Mobile Phone`
- `LATAM Mobile Phone`
- `Middle East & Africa Mobile Phone`
- `Mobile Phone (Every Provider)` — runs across the full provider set.

Choosing a region-specific version prioritizes the providers with the strongest coverage for that geography, which can improve match rates and reduce spend when you know where your contacts are located.

## Validation

Validation lets you verify each phone number before the waterfall accepts it, so you stop only on numbers that meet your quality bar — not just the first number any provider returns.

Validation is turned on by default in the Mobile Phone waterfall. Two phone validators are available for every `Optimized For` option:

- **Trestle — Verify phone number** *(selected by default)*
- **ClearoutPhone — Check phone line type & status**

Both validators run on Clay credits by default. Connecting your own Trestle or ClearoutPhone API key is optional. Each validator checks whether a candidate number is valid and what line type it is (for example, mobile, landline, or VoIP). Phone validators do **not** confirm that the number belongs to the specific person you're enriching — to check whether a number is likely to reach that person, use SureConnect's **Verify phone number** enrichment as a separate column (see [FAQs](#faqs)).

Whichever validator you use, two options control how validation behaves:

### Only validate mobile phone types?

By default, the validator returns **all phone line types — including landline and VoIP — as valid**. Enable this setting to consider **only mobile/cellular numbers as valid**; with it on, non-mobile line types will not pass validation, so the waterfall keeps mobile numbers only.

- **Enable** when you strictly need personal mobile numbers — for example, for SMS campaigns or dialing personal cells.
- **Leave off** to accept any valid phone line type.

`Only validate mobile phone types?` is off by default. How it filters depends on your validator:

- **Trestle (default validator):** turning on `Only validate mobile phone types?` is enough. Landline and VoIP numbers are rejected and the waterfall moves on to the next provider.
- **ClearoutPhone:** turn on **both** `Only validate mobile phone types?` and `Require validation success?`. With only `Only validate mobile phone types?` on, non-mobile numbers can still be kept.

Changing this setting doesn't update results already in your table. After you turn it on, click **Save**, then re-run the existing rows to apply it.

### Require validation success?

When enabled, the waterfall **only accepts a number that the validator explicitly confirms as valid**. If validation fails or is inconclusive, the number is rejected and the waterfall moves on to the next provider.

- **Enable** for the highest-quality output. This is stricter, so it may call more providers per contact and can lower your overall fill rate.
- **Disable** to have the waterfall accept a provider's number even when validation doesn't succeed. In this mode, validation acts as informational metadata rather than a gate that blocks results.

**Tip:** Enabling both options gives you the strictest result — only validated mobile numbers are kept. Loosening either option trades quality for higher coverage and lower credit spend.

## Additional column settings

These optional settings control how results and intermediate data appear in your table:

- **Output name of successful provider?** — When enabled, adds a column showing which provider returned the accepted number, so you can see source attribution per row.
- **Hide provider columns?** *(enabled by default)* — Hides the intermediate per-provider columns the waterfall uses internally, keeping your table clean. Disable this if you want to inspect the raw output of each provider.

## Finding a work (corporate) direct-dial phone number

Clay doesn't have a dedicated work-phone or direct-dial waterfall. Every preset Mobile Phone waterfall targets a person's mobile (cell) number. No single provider reliably finds a person's corporate direct-dial line, so the best way to get one is to chain several direct-dial providers as separate enrichment columns and then validate the numbers they return.

Providers that return phone numbers, such as Bytemine, require the Launch plan or above. See [Trial plan and provider restrictions](building-a-data-waterfall.md#trial-plan-and-provider-restrictions).

To build a custom direct-dial cascade:

1.  Click `Add enrichment` and add Bytemine's **Find contact info** enrichment. Turn on **Require direct dial**, and use its **Direct dial** output.
2.  Add SMARTe's **Enrich contact** enrichment, which returns **Direct dial**, **Direct dial 1**, and **Direct dial 2** fields. Under its run settings, turn on **Add run condition** so it runs only when the Bytemine **Direct dial** column is empty.
3.  Add a formula column that merges the results into one field, for example `{{Bytemine Direct dial}} || {{SMARTe Direct dial}}`.
4.  Validate the merged number with ClearoutPhone's **Check phone line type & status** or Trestle's **Verify phone number**. Both report whether the number is valid and what line type it is (for example, mobile or landline).

For the full run-condition pattern, see [Building a provider cascade with run conditions](building-a-data-waterfall.md#building-a-provider-cascade-with-run-conditions).

The inputs these direct-dial providers accept:

-   **Bytemine Find contact info**: any one of **Professional profile URL**, **Person's name**, **Email address**, or **Facebook profile URL**.
-   **SMARTe Enrich contact**: **Person's professional URL** on its own, or **Person's full name** plus **Company name** or **Company URL**.

Map the person's name, company, and professional profile URL when you have them, so each provider has an identifier it can match on.

## FAQs

**Do I have to use validation?**
No, but validation is on by default — the Mobile Phone waterfall selects Trestle as the validator automatically. You can remove the validator; without one, the waterfall accepts the first number any provider returns. Keeping a validator is recommended when number quality and line type matter.

**Which validators can I use, and do I need my own API key?**
Every Mobile Phone waterfall option, including `Mobile Phone (Global)` and the regional versions, offers two validators: Trestle's **Verify phone number** (the default) and ClearoutPhone's **Check phone line type & status**. Both run on Clay credits by default, so you don't need your own API key. You can optionally connect your own Trestle or ClearoutPhone account.

**Why is my Mobile Phone waterfall returning landline or VoIP numbers?**
When `Only validate mobile phone types?` is off (the default), the validator only checks that a number is real and valid, not that it's a mobile number. So a valid landline or VoIP number can end up in your Mobile Phone waterfall results. To keep only mobile numbers:

1.  Click the waterfall tab, select **Edit group**, and open the **Full configuration** tab.
2.  Under **Validation**, turn on `Only validate mobile phone types?`. If your validator is ClearoutPhone, also turn on `Require validation success?`.
3.  Click **Save**.
4.  Re-run your existing rows. Saving the setting doesn't change results that are already in your table.

**What's the difference between the two validation options?**
`Only validate mobile phone types?` filters by *line type* — enable it so only mobile/cellular numbers count as valid (by default, all line types, including landline, are considered valid). `Require validation success?` gates by *validation outcome* — keep only numbers the validator confirms valid. You can use them independently or together.

**Will stricter validation cost more credits?**
It can. Rejecting more numbers means the waterfall calls more providers per contact before it finds an acceptable result, which can increase spend and reduce fill rate — in exchange for higher-quality output.

**Some of the phone numbers the waterfall is returning are wrong or outdated — how do I find out which provider is responsible?**
Enable **Output name of successful provider?** in your waterfall's **Additional column settings**. This adds a column to your table showing which provider returned the accepted number for each row. When reps flag a bad number, check that column to identify a pattern — if the same provider appears repeatedly on flagged rows, that provider may have stale data for your specific audience or geography.

To compare providers directly before committing to a waterfall order, run individual provider enrichments on the same set of contacts rather than nesting waterfalls. Running them as separate columns makes each provider's result visible and attributable, so you can evaluate accuracy across sources side by side. Once you've identified which providers consistently return the most accurate results for your use case, reorder or disable underperformers in the waterfall's **Waterfall sequence** configuration (open via the waterfall tab → **Edit group** → **Full configuration** tab).

**The Mobile Phone waterfall didn't find a number, or the number is wrong — what else can I try?**
If the Mobile Phone waterfall comes back empty or returns an inaccurate number, try these options:

-   **Switch the `Optimized For` region** to match where your contacts are based (US & Canada, Europe, APAC, LATAM, or Middle East & Africa), or use `Mobile Phone (Every Provider)` to run across the full provider set. See [Optimize for (location)](#optimize-for-location).
-   **Add or reorder providers** in the **Waterfall sequence**. More providers means more chances to find a match.
-   **Keep validation on** so invalid numbers fail and the waterfall moves on to the next provider instead of keeping a bad result. See [Validation](#validation).
-   **Check that the number belongs to the person.** Phone validators (Trestle and ClearoutPhone) confirm that a number is valid and what line type it is, but not who it belongs to. To check whether a number is likely to reach the person you're enriching, add SureConnect's **Verify phone number** enrichment as a separate column after the waterfall. It takes the phone number and the person's full name (company name is optional). SureConnect can't be selected as a validator inside the waterfall, and its results arrive asynchronously. See [SureConnect integration](sureconnect-integration-overview.md).
-   **Search for a publicly listed number with Claygent.** Add a Claygent (AI web researcher) column that searches the web — for example the person's bio, their company website, or a business listing — for a published phone number. This can work well for small businesses whose numbers aren't in phone data providers' databases.
