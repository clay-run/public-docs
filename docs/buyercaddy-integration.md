---
title: BuyerCaddy integration
source_url: https://university.clay.com/docs/buyercaddy-integration
last_synced: 2026-04-26T01:39:42.591Z
upstream_hash: b2d04e5bb1149247190d5aadba8241c0e0ba8c80d43c212319bcc34033e09d4b
---

# BuyerCaddy integration

Enrich company tech stacks, verify technology usage, and more!

**BuyerCaddy** is a technographic intelligence platform providing real-time data on companies' technology stacks, covering over 95,000 IT products across millions of companies.

With this integration, you can enrich company tech stacks, verify technology usage, compare tech stack adoption against peer cohorts, and discover alternative or complementary technology products.

## Enriching data with BuyerCaddy

1.  While in a Clay table, click `Add enrichment` and search for `BuyerCaddy`.
2.  Under `Integrations`, select one of the BuyerCaddy options.
3.  In the modal, you will be asked to `Select BuyerCaddy account`.
    -   If you haven't already connected your BuyerCaddy account, click `+ Add account` and go through authentication.
    -   Get your API key from [buyercaddy.com/sign-up](http://buyercaddy.com/sign-up)

### `Action` Enrich company tech stack

Use this action to find a company's entire technology stack with optional filtering by product categories.

**Inputs**

-   **Company domain**
-   **Select categories (optional)**
-   **Limit (optional):** Maximum number of products to return. Defaults to 100.

### `Action` Verify technology usage

Use this action to check if a company is using specific products within their tech stack.

**Inputs**

-   **Company domain**
-   **Product IDs:** Array of BuyerCaddy product IDs to verify

### `Action` Compare company tech stack

Use this action to compare a company's usage of a specific product against peer cohorts.

**Inputs**

-   **Company domain**
-   **Product ID:** The specific product to analyze
-   **Cohort type:** Select comparison group:
    -   **Default** - Compare against similar companies (industry, size, region)
    -   **Competitors** - Compare against direct competitors
    -   **Custom** - Define your own peer group (if configured in BuyerCaddy)

### `Action` Find alternative or complementary technology products

Use this action to discover alternative or complementary products based on a company's current technology stack and competitive landscape.

**Inputs**

-   **Company domain**
-   **Product ID:** The anchor product to find alternatives/complements for
-   **Cohort type:** Comparison basis (Default, Competitors, or Custom)
-   **Relationship type (optional):** Specify whether you're looking for alternatives, complements, or both

### Run settings

-   **Auto-update:** By default, BuyerCaddy will auto-update enrichments every 24 hours.
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university))
