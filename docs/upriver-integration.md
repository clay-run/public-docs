---
title: Upriver integration
description: Use Upriver in Clay to find the brands sponsoring creators, pull brand product catalogs and product details, and research brand identities and audience personas.
last_synced: 2026-10-07T03:19:19.404Z
---

# Upriver integration

Map the sponsorships, products, and audiences behind any brand.

Upriver is a brand intelligence tool for researching the sponsorships, product catalogs, and audiences behind consumer and B2B brands. With this integration, you can find the brands sponsoring a creator's channel or newsletter, pull a brand's products and product pages, and research the personas a brand sells to.

## Enriching data with Upriver

1.  While in a Clay table, click `Add enrichment` and search for `Upriver`.
2.  Under `Integrations`, select one of the Upriver actions.
3.  In the modal, you will be asked to `Select Upriver account`.
    -   If you have your own account, click `+ Add account` and enter your Upriver API key. Otherwise, use the Clay provided key.

**Note:** The `Find sponsors` and `Find sponsorships` actions search either a publication or a set of categories. Fill in `Publication URL` or `Categories`, not both in the same run.

### `Action` Find sponsors

Search for the brands sponsoring a creator's channel or newsletter.

**Inputs**

Required — provide one:

-   **Publication URL:** The URL of a YouTube channel or newsletter.
-   **Categories:** The creator categories to search within. Set `Category search type` to `Browse categories` to pick from Upriver's own category list and narrow further with `Subcategories`, or set it to `Free text` to type your own keywords, which are matched to the closest categories automatically.
-   **Continue from previous response:** The page token from an earlier run, used to fetch the next page of sponsors.

Optional:

-   **Platforms:** The platforms to include in the search. If left empty, results include all available platforms.
-   **Sponsorship types:** Narrow results to `Explicit ad`, `Implicit ad`, `Affiliate`, `Promotion`, `Unknown`, `Merch store`, or `Self promotion`. Defaults to `Explicit ad`, `Promotion`, and `Unknown`.
-   **Category matches:** When searching by category, how many category matches to consider per query, from `1` to `10`. Defaults to `3`.
-   **Confidence threshold:** The minimum confidence a sponsorship needs to be returned, from `0` to `1`, where `1` is the highest confidence. Defaults to `0.5`.
-   **Include evidence:** Returns the source, excerpt, and confidence score behind the most recent ad. On by default.
-   **Limit:** How many sponsors to return, from `1` to `20`. Defaults to `10`.

**Outputs**

-   **Brand Name:** The name of the sponsoring brand.
-   **Sponsor Domain:** The brand's website domain.
-   **Sponsor professional profile:** The brand's professional social media profile URL.
-   **Total Ads Found:** How many ads Upriver has found for this brand.
-   **Most Recent Ad:** The brand's latest placement, including:
    -   **Creator Name** and **Channel URL**
    -   **Creator Categories** and **Platform**
    -   **Video URL** and **Published Date**
    -   **Sponsorship Type**
    -   **Evidence**, with a **Source**, **Excerpt**, and **Confidence Score**
-   **Total returned** and **Total available:** How many sponsors came back in this run, and how many Upriver has for the search overall.
-   **Primary industry category:** The industry category Upriver matched for the search.
-   **Page token for next result** and **Has more sponsors:** The two values you need to page through the rest of the results.

### `Action` Find sponsorships

Pull the individual sponsorship placements from a creator's channel or newsletter.

**Inputs**

Required — provide at least one:

-   **Sponsor name:** The name of the brand whose placements you want.
-   **Publication URL:** The URL of a YouTube channel or newsletter.
-   **Categories:** The creator categories to search within, either browsed from Upriver's list or typed as your own keywords.
-   **Continue from previous response:** The page token from an earlier run, used to fetch the next page of placements.

Optional:

-   **Platforms:** The platforms to include in the search. If left empty, results include all available platforms.
-   **Sponsorship types:** Narrow results to `Explicit ad`, `Implicit ad`, `Affiliate`, `Promotion`, `Unknown`, `Merch store`, or `Self promotion`. Defaults to every type except `Affiliate`.
-   **Category matches:** When searching by category, how many category matches to consider per query, from `1` to `10`. Defaults to `3`.
-   **Confidence threshold:** The minimum confidence a sponsorship needs to be returned, from `0` to `1`, where `1` is the highest confidence. Defaults to `0.5`.
-   **Days back:** How many days back to search, from `1` to `365`.
-   **Since date:** The start of the date range to search. Accepts most date formats, such as `2025-01-01` or `March 1, 2026`.
-   **Until date:** The end of the date range. Defaults to today.
-   **Include evidence:** Returns the source, excerpt, and confidence score behind each placement. On by default.
-   **Limit:** How many placements to return, from `1` to `20`. Defaults to `10`.

**Outputs**

-   **Sponsor Name:** The name of the sponsoring brand.
-   **Sponsor Domain:** The brand's website domain.
-   **Sponsor professional profile:** The brand's professional social media profile URL.
-   **Sponsorship Type:** Which kind of placement this was.
-   **Partner Confidence:** How confident Upriver is that the brand sponsored this piece of content.
-   **Publication Name**, **Publication URL**, **Publication Categories**, and **Platform:** The creator the placement ran with.
-   **Content URL** and **Published Date:** The specific video, episode, or issue the placement appeared in, and when it went out.
-   **Evidence:** The **Source**, **Excerpt**, and **Confidence** behind the placement.
-   **Total returned** and **Total available:** How many placements came back in this run, and how many Upriver has for the search overall.
-   **Page token for next result** and **Has more sponsorships:** The two values you need to page through the rest of the results.

### `Action` Find products

Return a brand's product catalog, with each product's name, category, description, and page URL.

**Inputs**

Required:

-   **Brand URL:** The brand's website, such as `https://nike.com`.

Optional:

-   **Brand name:** The brand's name. Resolved from the URL if you leave it empty.
-   **Continue from previous response:** The page token from an earlier run, used to fetch the next page of products.
-   **Limit:** How many products to return, from `5` to `20`. Defaults to `10`.

**Outputs**

-   **Brand URL** and **Brand name:** The brand Upriver matched.
-   **Products:** One entry per product, each with a **Product name**, **Category**, **Description**, and **Product URL**.
-   **Total count:** How many products Upriver found for the brand.
-   **Page token for next result** and **Has more products:** The two values you need to page through the rest of the catalog.

### `Action` Get product details

Research a single product in depth, including its description, features, and pricing.

**Inputs**

Required:

-   **Product name:** The name of the product to look up.
-   **Brand URL or Brand name:** The brand that makes it. A URL gives Upriver the most to work with, but either one will identify the brand.

Optional:

-   **Product URL:** The product's own page URL. Recommended for accuracy.

**Outputs**

-   **Product name** and **Description:** The product Upriver matched, and what it is.
-   **Features:** The product's selling points, one per entry.
-   **Specifications:** The product's technical specifications.
-   **Price** and **Currency:** What the product sells for, and in which currency.
-   **Reviews summary:** A summary of the product's customer reviews, including its rating where one is published.
-   **Alternatives:** Competing products a buyer would compare this one against.
-   **Images:** Image URLs from the product's page.

### `Action` Get brand details

Research a brand's identity, including its positioning, industries, and the audience it sells to.

**Inputs**

Required — provide at least one:

-   **Brand URL:** The brand's website. This gives Upriver the most to work with.
-   **Brand name:** The brand's name. Can be used alongside `Brand URL`.

**Outputs**

-   **Brand name** and **Brand URL:** The brand Upriver matched, each with a **Name reason** and **URL reason** explaining the match.
-   **Brand note:** A one-line summary of what the brand does.
-   **Mission**, **Values**, and **Tagline:** The brand's stated positioning, each with a matching **Mission reason**, **Values reason**, and **Tagline reason**.
-   **Tone** and **Key phrases:** How the brand writes about itself and the phrases it returns to, with a **Tone reason** and **Key phrases reason**.
-   **Brand colors:** The brand's **Primary colors** and **Secondary colors**, as hex values.
-   **Industries:** The industries the brand operates in.
-   **Audience description:** Who the brand sells to, with an **Audience reason**.
-   **Effort level:** The research depth used for the lookup.

### `Action` Get audience personas

Build out the personas within a brand's audience, including what moves them to buy and what holds them back.

**Inputs**

Required:

-   **Brand URL:** The brand's website.

Optional:

-   **Search query:** Narrows the research to one topic or angle within the brand's audience. Searching `running shoes for beginners` surfaces entry-level runner personas, where `streetwear fashion` surfaces style-driven ones. Leave it empty to explore the brand broadly.
-   **Include citations:** Returns real-world quotes from online discussions that back up each persona. On by default.

**Outputs**

-   **Rollup summary:** A single summary of the brand's audience across every persona returned.
-   **Personas:** One entry per persona, each with:
    -   **Label** and **Description**
    -   **Personality traits**, each with a **Trait ID** and **Trait label**
    -   **Purchase triggers** and **Purchase barriers**
    -   **Behaviors** and **Phrase examples**
    -   **Voice and tone**
    -   **Citations**, each with a **Title**, **Excerpt**, **Source URL**, and **Subreddit**
-   **Persona count:** How many personas the run returned.
-   **Metadata:** Includes **Generated at**, the date the personas were produced.

### Run settings

-   **Auto-update:** Recommended when you want a table to keep tracking a brand's placements or catalog as Upriver finds new ones.
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

## FAQs

### How do I get more than 20 results?

The three search actions return at most 20 results per run, so larger lists are built a page at a time. Check the `Has more sponsors`, `Has more sponsorships`, or `Has more products` output after a run — when it comes back true, add a second column with the same action and pass that run's `Page token for next result` into `Continue from previous response`.

These three actions charge per result returned, so a higher `Limit` costs more than a lower one.

### What's the difference between Find sponsors and Find sponsorships?

`Find sponsors` returns one row per brand, with a count of every ad Upriver has found for it and the details of its most recent placement. `Find sponsorships` returns one row per individual placement, so the same brand can appear several times, and it takes a date range so you can look at a specific window.

Reach for the first to build a list of brands worth approaching, and the second to track placements over time.

### How far back can Find sponsorships look?

`Since date` accepts any date within the past year, and `Until date` has to be today or earlier. Setting either one overrides `Days back`, so use `Days back` on its own when a rolling window from today is all you need.

### Why did a run finish without returning any data?

When Upriver has no match for the brand, product, or publication you gave it, the action finishes successfully with an empty result rather than failing. Runs that finish without data are refunded, so a miss costs you nothing.
