---
title: SE Ranking integration
description: Use SE Ranking in Clay to enrich tables with AI search visibility metrics, organic traffic estimates, ad spend data, and competitor information.
last_synced: 2026-07-15T20:50:43.132Z
---

# SE Ranking integration

Enrich your data with AI search visibility metrics, traffic estimates, ad spend data, and organic competitor information.

SE Ranking is an SEO and SEM intelligence platform for tracking search visibility and competitive analysis. With this integration, you can enrich your data with AI search visibility metrics, traffic estimates, ad spend data, and organic competitor information.

## Enriching data with SE Ranking

1.  While in a Clay table, click `Add enrichment` and search for `SE Ranking`.
2.  Under `Integrations`, select one of the SE Ranking options.
3.  In the modal, you will be asked to `Select SE Ranking account`.
    -   Clay provides a shared API key for all users. If you prefer to use your own SE Ranking account, click `+ Add account` and go through authentication.

### `Action` Get AI search visibility

Retrieve AI search visibility data showing how a domain appears across major language models including ChatGPT, Perplexity, Gemini, Google AI Overviews, and AI Mode.

**Inputs**

Required:

-   Domain/URL: The target domain or URL to analyze.
-   LLM: Which language model(s) to check. Options: All LLMs, ChatGPT, Perplexity, Gemini, AI Overviews, AI Mode.
-   View: Choose between Snapshot (current data) or Time Series (historical trend).
-   Region: Country code for regional results (default: `us`).

Optional:

-   Brand: Specify a brand name to filter results.
-   Scope: How to interpret the domain input. Options: `base_domain` (default), `domain`, `url`.

**Outputs**

-   Brand presence: Number of times the brand appears in AI responses.
-   Link presence: Number of times the domain is linked in AI responses.
-   Average position: Mean ranking position across AI results.
-   Share of voice: Percentage of visibility compared to competitors.
-   Time series data: Historical visibility trends (when Time Series view is selected).

### `Action` Get traffic and ad spend

Get organic and paid traffic estimates plus ad spend for a target domain.

**Inputs**

Required:

-   Domain/URL: The target domain to analyze.
-   Region: Choose `Worldwide` or specify a country code (default: `Worldwide`).

Optional:

-   Currency: Currency for ad spend data (default: USD). Applies in Worldwide mode only.
-   Include subdomains: Set to `true` to include subdomain traffic in results (default: true).
-   Type: Filter by traffic type — `Organic` or `Paid`. Applies in regional mode only.

**Outputs**

-   Organic traffic: Estimated monthly organic search traffic.
-   Paid traffic: Estimated monthly paid search traffic.
-   Ad spend: Estimated monthly advertising spend.
-   Traffic sources: Breakdown by search engine and geography.
-   Traffic trends: Month-over-month traffic changes.

### `Action` Get organic competitors

Identify top organic or paid search competitors for a given domain.

**Inputs**

Required:

-   Domain: The target domain to analyze.

Optional:

-   Region: Country code for regional competitor analysis (default: `us`).
-   Type: Choose between Organic or Paid competitors.

**Outputs**

-   Competitor domains: List of competing domains.
-   Overlap score: Percentage of shared keywords with the target domain.
-   Visibility score: Estimated search visibility for each competitor.
-   Common keywords: Number of overlapping keywords.
-   Traffic estimate: Estimated monthly traffic for each competitor.

### Run settings

-   Auto-update: Enable this to automatically refresh SE Ranking data when the source records update. Useful for maintaining current AI visibility scores or tracking competitor changes over time.
-   Only run if: Use [**conditional formulas**](https://university.clay.com/) to control when the action runs. For example, only check AI visibility for domains with high organic traffic, or only fetch competitor data for accounts in your target segment.

## Best practices

-   Use AI visibility as an ICP signal: Brands with strong AI search presence may be more digitally sophisticated and open to modern GTM tools.
-   Qualify by traffic volume: Filter for domains with meaningful traffic before enriching with deeper competitor or ad spend data.
-   Track competitors over time: Enable auto-update on the `Get organic competitors` action to monitor when new competitors emerge in your target accounts' space.
-   Combine with firmographic data: Cross-reference AI visibility scores with company size, industry, and funding to identify high-fit prospects.
