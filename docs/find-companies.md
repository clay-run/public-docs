---
title: Find Companies in Clay
source_url: https://university.clay.com/docs/find-companies
description: Find companies that match your specific criteria within Clay's
  proprietary dataset.
last_synced: 2026-04-26T01:39:58.486Z
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
    -   **Company size** — The self-reported size band on the company's profile (e.g., 11–50, 51–200). Select one or more bands from the dropdown.
    -   **Annual revenue ranges** — Filter by revenue brackets from $0–$500K up to $100B+.
    -   **Funding amount**
    -   **Company types** — Privately Held, Public Company, Partnership, Self Employed, Non Profit, Educational, Self Owned, or Government Agency.
    -   **Keywords** to include or exclude
        -   **Exact phrase matching:** Wrap multi-word terms in single or double quotes to search for that exact phrase. For example, searching for "Google Cloud" finds companies with "Google Cloud" in their description — not just companies that mention Google and cloud separately. Note: Special characters (#, +, !) and stopwords ('a', 'an', 'of', 'the') are stripped out even with quoted phrases.
    -   **Semantic company description** — Enter a free-text description to help rank results based on how closely they match your ideal company profile (e.g., "B2B fintech company selling to mid-market banks").
    -   **Location** — Filter by country, and separately by city or state. Both support include and exclude.
    -   **Estimated employee count** — Filter by a numeric count of estimated employees (enter a minimum and/or maximum). This is a separate field from **Company size** — see the [FAQ below](#why-do-company-sizes-and-estimated-employee-count-return-different-results-for-the-same-range) for why the same numeric range can surface different companies.
    -   **AI filters** — Clay-generated attributes applied to company profiles:
        -   **Industries** and **Subindustries** (include or exclude)
        -   **Revenue streams** — e.g., Subscriptions/Recurring, Professional Services, Transaction Fees, Advertising, Licensing/IP
        -   **Business types** — B2B, B2C, or Nonprofit
    -   **Technographics** — Filter by installed technology, powered by [BuyerCaddy](https://university.clay.com/docs/buyercaddy-integration). Costs **3 credits per matching company row** — cheaper in most cases than pulling a broad list and running a technographic enrichment afterward, since you pay only for companies that already match your tech criteria. Technographics data is also included when sending company rows to Audiences; the same 3-credit cost per matching row applies.
        -   **Vendors** — e.g., AWS, Salesforce, HubSpot
        -   **Products** — e.g., Amazon EC2, Salesforce Sales Cloud
        -   **Main categories** and **Parent categories**
        Product and vendor names in the filter come from BuyerCaddy's catalog and may not match a company's public brand name exactly. To identify what a product name refers to, run the search and check the **Vendor** field in the cell details for any returned row — it shows the company behind the product.
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

**Outputs:**

Each result includes one or more **Structured Location** entries in the cell details with geocoded, normalized fields — so you don't need additional AI columns to parse or reformat location data. These fields work with informal location names like "Greater Chicago Area." Use **Is Headquarters** to identify the company's primary location when multiple entries are returned.

-   **City**
-   **State**
-   **Region**
-   **Country Iso**
-   **Postal Code**
-   **Is Headquarters**

## FAQs

### Can I filter by job title or role in company search?

No — `Find Companies` only filters by company-level attributes (industry, size, location, revenue, etc.). There is no job title filter in company search. Job title is a person-level attribute available only in People search.

**To find people with specific roles (e.g., CEO, Founder, Owner) at companies in your list, you have two options:**

-   **From your company table** — Click **Tools** (or **Actions**) → **Find People at These Companies**. Under **Job title keywords**, enter your target titles comma-separated (e.g., `CEO, Founder, Owner, Co-founder`). This returns only those roles at the companies already in your table.
-   **Start a fresh People search** — Click `+ Add` at the bottom of your workbook, search for `Find People`, and use the **Job title** filter alongside company attributes (industry, size, location).

For more detail on both workflows, see [Guide: Finding companies and people in Clay](finding-companies-and-people-in-clay.md).

### Can I filter companies by the year they were founded?

Founded year is not available as a filter when building a `Find Companies` search — you can't narrow results by founding date before importing.

However, `Find Companies` automatically includes a **Founded** column in your table showing the founding year for each company. Once you've imported your results, you can filter or sort that column to focus on companies founded within a specific range — for example, filtering to companies founded after 2020 to target early-stage startups.

### Does importing from Find Companies cost credits?

**No, unless you use technographics filters.** Importing companies using standard filters — industry, size, location, revenue, company type, AI filters — consumes no Actions and no Data Credits.

If you enable **technographics filters**, each company row that matches your criteria costs **3 Data Credits**.

Any enrichments you add to the table afterward (e.g., finding emails, enriching headcount) consume their own Actions and Data Credits as usual — only the import itself is free.

### Why does my table show fewer rows than the preview count?

**The import may still be in progress.** Find Companies imports process asynchronously — rows are added in batches. If you check right after clicking Import, the row count will be lower than the final total. Wait a minute and refresh to see the complete count.

If the count still doesn't match after the import finishes, the **preview count** (e.g., "Showing 50 of ~39,869 results") is an approximate figure — the `~` tilde prefix in the UI indicates the total is estimated using a fast approximate count, not an exact query. The actual import can return a slightly different total, and this is normal.

Also check your **Limit results** setting: the import won't exceed whatever limit you've configured (default 10,000).

### Why do Company sizes and Estimated employee count return different results for the same range?

These two filters measure different things:

-   **Company sizes** is a dropdown that selects categorical size bands — 11–50, 51–200, 201–500, etc. — reflecting the size range a company has reported on its profile.
-   **Estimated employee count** is a numeric min/max filter based on a separately computed count of estimated employees derived from profile data.

Because the two values are sourced independently, a company whose reported size band is "51–200" may have a computed employee count of 250 — or vice versa. Filtering on one versus the other can return a different set of companies even when the numbers appear to overlap.

### Re-running Find Companies shows far fewer results than my original run

This is expected behavior. The Find Companies source deduplicates new results against rows already in your table — re-running returns only the net-new companies not yet present in the table.

**Example:** If your table already has 29,000 companies from a previous import, re-running with the same filters returns only the companies genuinely new since the last run — for example, 32 new companies. The existing 29,000 remain in your table; they are not replaced or removed.

Deduplication is based on each company's unique profile ID, not your filter configuration. A company already in the table is skipped on re-run regardless of whether your filters changed.

**To re-import the full result set** (for example, when testing): delete the existing rows from your table first, then re-run the source. Once the rows are cleared, the search re-imports all matching companies from scratch.
