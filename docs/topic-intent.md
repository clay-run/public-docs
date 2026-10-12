---
title: Topic Intent
description: Find net-new companies and people actively researching topics relevant to your business, using intent data from Bombora, Delivr, and Intentsify. Currently in open beta, available on all paid plans.
---

# Topic Intent

Topic Intent is a source that finds net-new companies or people actively researching topics relevant to your business. Clay checks for intent signals across Bombora, Delivr, and Intentsify and returns results with per-provider scores so you can see exactly where each signal came from.

**Topic Intent is currently in open beta and available on all paid plans.**

Common use cases:

-   **Prioritize in-market accounts.** Layer intent into lead scoring so reps focus on accounts already researching your category.
-   **Find net-new buyers.** Source companies or people researching a competitor, product category, or industry theme.
-   **Build higher-intent ad audiences.** Sync people and accounts showing fresh intent into LinkedIn, Meta, or Google Ads.
-   **Personalize outreach.** Use the specific topic someone is researching to tailor messaging at the account or person level.

## Finding net-new companies with topic intent

Topic Intent returns company-level results — one row per matching company, with domain, name, and per-provider intent scores.

**To set up Topic Intent in a workbook:**

1.  Click `+ Add` at the bottom of the workbook.
2.  Search for `topic intent` in the **Create new table** dialog.
3.  Select **Topic intent** (or the **Get net-new accounts with topic intent** template).
4.  Choose the **Companies** entity if prompted.
5.  Select one or more **Topic intent providers** (Bombora, Delivr, and/or Intentsify).
6.  Select **Intent topics** — the topics you want to track. Limits vary by provider: up to **25 topics for Delivr**, up to **50 topics for Bombora or Intentsify**.
7.  Configure optional filters (see [Filter options by provider](#filter-options-by-provider) below).
8.  Set the **Company limit** (default: 100).
9.  Click **Preview** and then **Import to new table**.

**To add Topic Intent as a source to an existing table:**

1.  In your table, click `Tools` → `Import`.
2.  Search for `topic intent` and follow steps 4–9 above.

## Finding net-new people with topic intent

Topic Intent returns person-level results — one row per matching person, with hashed email (HEM), professional URL, email (where available), and per-provider intent scores. Delivr and Intentsify support person-level results; Bombora returns company-level only.

1.  Click `+ Add` at the bottom of the workbook.
2.  Search for `topic intent` and select **Topic intent**.
3.  Choose the **People** entity.
4.  Select **Topic intent providers** (Delivr and/or Intentsify — Bombora is not available for people).
5.  Select **Intent topics** (up to 25 for Delivr, up to 50 for Intentsify).
6.  Configure optional filters.
7.  Set the **People limit** (default: 100).
8.  Click **Preview** and then **Import to new table**.

## Filter options by provider

Not all filters apply to every provider. The table below shows which filters each provider supports:

| Filter | Delivr | Bombora | Intentsify |
|---|---|---|---|
| Intent score tiers | ✓ (medium and high only) | ✓ | ✓ |
| Timeframe (days) | — | ✓ | ✓ |
| Minimum people count | ✓ | — | — |
| Company size | — | ✓ | — |
| Industry | — | ✓ | — |
| Metro area | — | ✓ | — |
| Research stage | — | — | ✓ |
| Country | — | — | ✓ |
| Region / State | — | — | ✓ |
| City | — | — | ✓ |

**Intent score tiers:** Choose Low, Medium, or High intent. Defaults to **Medium and High**. Delivr returns only medium and high intent results — selecting Low has no effect on Delivr.

**Timeframe:** How many days of intent history to include. Defaults to **30 days** (applies to Bombora and Intentsify). Delivr does not use a timeframe filter.

**Research stage (Intentsify only):** Filter by **Early** or **Late** research stage, or leave as **Any stage**.

## Provider comparison

| Provider | Companies | People | Topic limit | Geographic coverage |
|---|---|---|---|---|
| Delivr | ✓ | ✓ | 25 | North America (at launch) |
| Bombora | ✓ | — | 50 | North America (at launch) |
| Intentsify | ✓ | ✓ | 50 | North America (at launch) |

Selecting multiple providers returns a merged result set: a company (or person) found by more than one provider appears once, with scores from each provider shown in the **Provider scores** field.

## Understanding the results

Each result row includes:

-   **Domain** (companies) or **Professional URL** / **Email** (people) — the primary identifier
-   **Company name** and **Industry** (companies)
-   **Provider scores** — an object with a sub-entry for each provider that matched:
    -   **Intent tier** — `high`, `medium`, or `low`
    -   **Raw score** — the provider's numeric score
    -   **Topic count** — how many of your selected topics matched
    -   **Topics** — the individual topic names and per-topic scores

## FAQs

### Does Topic Intent return company-level or person-level results?

It depends on which source you set up:

-   **Topic intent → Companies:** Returns company-level results (one row per matching company).
-   **Topic intent → People:** Returns person-level, de-anonymized results — name, title, and email where available.

### Which providers are available for people vs. companies?

Delivr and Intentsify return both company-level and person-level results. Bombora returns company-level results only.

### Can I use multiple providers at the same time?

Yes. When you select more than one provider, Clay queries all selected providers and merges results by company domain. A company found by multiple providers appears as a single row with scores from each provider visible in **Provider scores**.

### What does "low intent" mean?

Low intent indicates early-stage research signals — lower confidence that the company is actively evaluating. Medium and high intent indicate stronger in-market activity. Delivr returns only medium and high intent results; selecting Low has no effect when Delivr is the only provider.

### What geographic coverage does Topic Intent have?

At launch, Topic Intent is **North America-first**. Broader geographic coverage is planned for the future.

### Do I need to connect my own Bombora, Delivr, or Intentsify account?

No. Topic Intent runs on Clay credits — no separate provider accounts or API keys are required.

### Can I use Topic Intent to check intent for companies already in my table?

Yes, as an enrichment. Instead of adding Topic Intent as a source, add **Find company topic intent** (Delivr), **Find company topic intent** (Bombora), or the Intentsify equivalent as an enrichment column in your existing company table. This checks whether each company in your table is showing intent on your selected topics, rather than discovering new companies.

### How is Topic Intent different from Signals?

Topic Intent is a **source** — it finds net-new companies or people you don't already have in Clay. [Signals](signals.md) are **monitors** — they watch companies or contacts already in your table for changes like new hires, promotions, or job changes. Topic Intent can also be used as a signal inside Audiences to trigger on companies showing fresh topic intent — see your Audiences settings for details.
