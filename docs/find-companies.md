---
title: Find Companies in Clay
source_url: https://university.clay.com/docs/find-companies
last_synced: 2026-04-26T01:39:58.486Z
upstream_hash: 7b9393243aee046995c8e9efa8d82b2c48893e2def2a9c3c758b332a399f6c12
---

# Find Companies in Clay

Find companies that match your specific criteria within Clay's proprietary dataset.

The `Find Companies` source lets you build targeted lists of companies using filters like industry, size, location, and keywords.

It's perfect for creating sales prospect lists, identifying competitors, and conducting market research.

## **Creating a table with Find Companies**

1.  In a workbook, click `+ Add` at the bottom.
2.  Search for `Find Companies`.

## `Source` **Find Companies**

1.  Configure the source to your preferences:
    -   **Industries** to include and exclude
    -   **Company size**
    -   **Annual revenue ranges** — Filter by revenue brackets from $0–$500K up to $100B+.
    -   **Funding amount**
    -   **Company types** — Privately Held, Public Company, Partnership, Self Employed, Non Profit, Educational, Self Owned, or Government Agency.
    -   **Keywords** to include or exclude
        -   **Exact phrase matching:** Wrap multi-word terms in single or double quotes to search for that exact phrase. For example, searching for "Google Cloud" finds companies with "Google Cloud" in their description — not just companies that mention Google and cloud separately. Note: Special characters (#, +, !) and stopwords ('a', 'an', 'of', 'the') are stripped out even with quoted phrases.
    -   **Semantic company description** — Enter a free-text description to help rank results based on how closely they match your ideal company profile (e.g., "B2B fintech company selling to mid-market banks").
    -   **Location** — Filter by country, and separately by city or state. Both support include and exclude.
    -   **Minimum member count** / **Maximum member count** — Filter by the number of LinkedIn members associated with the company.
    -   **AI filters** — Clay-generated attributes applied to company profiles:
        -   **Industries** and **Subindustries** (include or exclude)
        -   **Revenue streams** — e.g., Subscriptions/Recurring, Professional Services, Transaction Fees, Advertising, Licensing/IP
        -   **Business types** — B2B, B2C, or Nonprofit
    -   **Technographics** — Filter by installed technology, powered by [BuyerCaddy](https://university.clay.com/docs/buyercaddy-integration). Costs **3 credits per matching company row** — cheaper in most cases than pulling a broad list and running a technographic enrichment afterward, since you pay only for companies that already match your tech criteria. Technographics data is also included when sending company rows to Audiences; the same 3-credit cost per matching row applies.
        -   **Vendors** — e.g., AWS, Salesforce, HubSpot
        -   **Products** — e.g., Amazon EC2, Salesforce Sales Cloud
        -   **Main categories** and **Parent categories**
    -   **Domain filters:**
        -   **Has domain** — Whether a company has a resolved domain.
        -   **Domain is live** — Whether the company's domain is currently active.
        -   **Domain redirects to another domain** — Whether the domain redirects elsewhere.
    -   **Exclude companies:** Exclude up to 3 different sets of companies from your search using Clay tables, CSVs, or manual lists. You can exclude up to 300,000 companies total (100,000 per source). Exclusions require a domain or LinkedIn URL.
    -   **Limit results** — Defaults to 10,000. Maximum 10,000.
2.  Click `Preview companies` and `Import to new table` when the results look good.
3.  Select import options:
    -   Add additional enrichments like `Company Headcount Growth` or `Most Recent News`.
    -   Enable or disable auto-update and auto-dedupe.
4.  Click `Continue`.
