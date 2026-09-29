---
title: G2 integration
description: Find products, competitors, ratings, features, and reviews from G2 — the world's largest software marketplace — to power competitive intelligence and go-to-market decisions in Clay.
last_synced: 2026-09-29T00:00:00.000Z
---

# G2 integration

Find products, competitors, ratings, features, and reviews from G2 — the world's largest software marketplace — to power competitive intelligence and go-to-market decisions in Clay.

G2 is the world's largest software marketplace. With this integration you can find products by domain or category, retrieve product ratings and features, pull customer reviews, and find competing products. Source actions for buyer intent signals are currently in beta.

## Using G2 in Clay

1.  While in a Clay table, click `Add enrichment` and search for `G2`.
2.  Under `Integrations`, select one of the G2 actions.
3.  Most G2 actions run on Clay's managed access and do not require you to connect an account. The **Find companies with G2 Buyer Intent** action requires a G2 API key — click `+ Add account` and enter your key to enable it.

### `Action` Find products

Find G2 products by domain, name, category, or minimum star rating. Returns product ID, name, description, website, slug, star rating, and review count. Use the returned product ID or slug as an input for the competitor, ratings, features, reviews, and buyer intent actions.

**Inputs** (provide at least one)

-   **Company domain** — finds products whose G2 detail URL contains this domain
-   **Search query** — full-text search across product names and descriptions
-   **Category**
-   **Minimum star rating**

### `Action` Find product competitors

Find competing products on G2 for a given product, including product ID, description, domain, G2 URL, star rating, and review count.

**Inputs**

-   **Product ID or slug (Required):** Use the Find products action to get a product ID or slug.

### `Action` Get product ratings

Get G2 ratings across seven categories: ease of use, quality of support, ease of setup, ease of doing business with, meets requirements, ease of admin, and moving in the right direction.

**Inputs**

-   **Product ID or slug (Required)**

### `Action` Get product features

Find the list of features associated with a G2 product, including feature ratings and verification status.

**Inputs**

-   **Product ID or slug (Required)**

### `Action` Get product reviews

Find G2 reviews for a product, including what users love, what they dislike, recommendations, benefits realized, and star rating.

**Inputs**

-   **Product ID or slug (Required)**

**Pricing:** You are charged per review returned. Market intelligence reviews (which include pricing, contract length, ROI timeframe, implementation cost, switching reasons, and reviewer firmographics) are charged at a higher rate. Enable **Market Intelligence** in the action settings to return these additional fields.

### `Source` Find companies with G2 Market Signals

Build a list of companies showing buyer intent on G2 categories. Returns one row per buyer intent interaction, including the company name, domain, category, and the date range the signal covers.

**Currently in beta — contact support to enable.**

**Inputs** (at least one required)

-   **Categories:** G2 product categories to monitor for buyer intent.
-   **Start date / End date:** Date range to check for signals (YYYY-MM-DD). Defaults to today.

### `Source` Find companies with G2 Buyer Intent

Build a list of companies researching your G2 products, with their activity and visitor counts. Query one product or several in a single run. Group by company for a summary or by day, week, or month for a time series.

**Currently in beta — contact support to enable.**

**Inputs**

-   **Product IDs or slugs (Required):** One or more G2 product UUIDs or slugs. Use the Find products action to get these.
-   **Group by (Required):** How to group the intent data. Choose at least one dimension — company name and domain give one row per company; add day, week, or month for a time series.

**Note:** This action requires a G2 API key. Click `+ Add account` to connect your G2 account before using it.
