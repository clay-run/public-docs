---
title: G2 integration
description: Find G2 products, competitors, reviews, ratings, features, and buyer intent signals.
last_synced: 2026-09-29T00:00:00.000Z
---

# G2 integration

Find G2 products, competitors, reviews, ratings, features, and buyer intent signals.

G2 is the world's largest software review marketplace. Through this integration, you can source companies showing buyer intent for software categories, find and compare products, retrieve ratings and reviews, and identify competitors — all directly in Clay.

## **Finding companies with G2**

G2 offers two sources that add new rows to a Clay table based on buyer intent signals. To use either source, click **Add source** in a Clay table (or select it when creating a new table), then search for and select the relevant G2 source.

### `Source` Find companies with G2 Buyer Intent

Build a list of companies researching your G2 products, with their activity and visitor counts. Query one product or several in a single run. Group by company for a summary or by day, week, or month for a time series.

**Authentication:** This source requires your own G2 API key with Buyer Intent access — Clay does not provide a shared key. Click **+ Add account** in the setup modal and enter your key.

**Inputs**

- **Product IDs or slugs (required):** One or more G2 product UUIDs or slugs (e.g. `hubspot-sales-hub`) to pull buyer intent for. Use the **Find products** enrichment to look up a product ID or slug.
- **Group by (required):** How to group the intent data. Company name and domain give one row per company; add day, week, or month for a time series.
- **Metrics (required):** Which aggregated metrics to return for each group (e.g. total activity).
- **Company name contains (optional):** Only return companies whose name contains this text.
- **Start date / End date (optional):** Date range for intent data (YYYY-MM-DD format).

### `Source` Find companies with G2 Market Signals

Build a list of companies showing buyer intent on G2 categories. Returns one row per buyer intent interaction, including the company name, domain, category, and the date range the signal covers.

**Cost:** 12 credits per signal returned. Successful searches that return no results are not billed.

**Inputs**

- **Categories (required):** One or more G2 categories to check for buyer intent signals.
- **Start date / End date (optional):** Date range to check for signals (YYYY-MM-DD). Defaults to today.
- **Maximum results (optional):** Maximum number of signals to return (1–25,000). Defaults to 1,000.

## **Enriching data with G2**

To use G2 enrichment actions, click **Add enrichment** in a Clay table and search for `G2`. All enrichment actions below use Clay's provided G2 key — no API key of your own is required.

### `Action` Find products

Find G2 products by name, category, or domain. Returns product ID, name, description, website, slug, star rating, and review count. Use this action to look up the product ID or slug required by the other G2 enrichment actions.

**Cost:** 2 credits per result.

**Inputs**

- **Company domain (optional):** Find products by the vendor's website domain, e.g. `salesforce.com`.
- **Search query (optional):** Full-text search across product names and descriptions, e.g. `email marketing`.
- **Product name (optional):** Product name to match; partial match by default. Enable **Use exact match** for an exact name search.
- **Vendor name (optional):** Vendor/company name to match.
- **Product IDs or Slugs (optional):** Look up specific products by their G2 UUID or slug.
- **Category (optional):** Filter results to a specific G2 category.
- **Minimum star rating (optional):** Only return products at or above this rating.
- **Maximum results (optional):** How many products to return.

_At least one of company domain, search query, product name, vendor name, product IDs, or slugs is required._

### `Action` Get product reviews

Find G2 reviews for a product, including what users love, what they dislike, recommendations, benefits realized, and star rating. Enable **Return market intelligence data** to return pricing, contract length, ROI timeframe, implementation cost, switching reasons, and reviewer firmographics instead.

**Cost:** 8 credits per review (standard). Market intelligence reviews are charged at a higher rate per review.

**Inputs**

- **Product ID or slug (required):** The G2 product UUID or slug to get reviews for (e.g. `hubspot-sales-hub`). Use **Find products** to look this up.
- **Return market intelligence data (optional):** When enabled, returns market intelligence fields instead of standard review fields.
- **Company segment (optional):** Only return reviews from reviewers in selected company segments.
- Filters for region, reviewer role, NPS score, date range, and result limit are also available.

### `Action` Get product ratings

Get G2 ratings across seven categories: ease of use, quality of support, ease of setup, ease of doing business with, meets requirements, ease of admin, and moving in the right direction.

**Cost:** 7 credits per result.

**Inputs**

- **Product ID or slug (required):** The G2 product UUID or slug to get ratings for.
- **Rating categories (optional):** Which of the seven rating categories to return. Leave empty to return all seven.

### `Action` Get product features

Find the list of features associated with a G2 product, including ratings and verification status.

**Cost:** 5 credits per result.

**Inputs**

- **Product ID or slug (required):** The G2 product UUID or slug to get features for.
- **Category (optional):** Filter features to a specific G2 category. Useful for products that span multiple categories.
- **Functionality (optional):** Filter by functionality type, e.g. `native` for natively supported features only.

### `Action` Find product competitors

Find competing products on G2 for a given product, including product ID, description, domain, G2 URL, star rating, and review count.

**Cost:** 3 credits per competitor returned. Maximum 50 competitors, default 10.

**Inputs**

- **Product ID or slug (required):** The G2 product UUID or slug to find competitors for.
- **Category (optional):** Narrow competitors to a specific G2 category. Useful when a product spans multiple categories.
- **Maximum results (optional):** Maximum number of competitors to return (1–50). Defaults to 10.

## FAQs

### Do I need a G2 API key?

It depends on which action you use. The **Find companies with G2 Buyer Intent** source requires your own G2 API key with Buyer Intent access — Clay cannot provide a shared key for this action. All other G2 actions (Market Signals, Find products, Get product reviews, Get product ratings, Get product features, Find product competitors) use Clay's provided key, so no personal API key is required.

### How do I find a product ID or slug to use with reviews, ratings, features, and competitors?

Use the **Find products** enrichment first — search by company domain, product name, or search query. The action returns each product's ID and slug, which you can then pass to the other G2 enrichment actions.

### What is the difference between G2 Buyer Intent and G2 Market Signals?

**G2 Buyer Intent** shows you companies actively researching *your specific products* on G2. It requires your own G2 API subscription and is ideal for sellers who want to identify warm accounts. **G2 Market Signals** shows companies researching a *software category* broadly, using Clay's key, and is useful for finding prospects who are in the market for a class of product without needing a G2 subscription.
