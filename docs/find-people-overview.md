---
title: Find People in Clay
source_url: https://university.clay.com/docs/find-people-overview
description: Discover relevant contacts matching your criteria within Clay's database, then enrich results with work email and mobile phone waterfalls.
last_synced: 2026-04-26T01:39:58.803Z
---

# Find People in Clay

Discover relevant contacts matching your criteria within Clay's database.

The `Find People` source helps you search for people using criteria like job title, company, location, and experience.

This tool is ideal for building targeted sales prospect lists, identifying potential hires, and conducting market research.

**Note:** You can get up to 500 results per cell by reducing the data you're requesting. Click the column name and select **Edit column → Reduce Data for More Results**.

## **Creating a table with Find People**

1.  In a workbook, click `+ Add` at the bottom.
2.  Search for `Find People`.

**Note:** The search wizard shows a preview of up to 50 results so you can check your criteria before importing. When you click **Import**, all matching results — up to the **Limit results** value you configure — are added to the table.

## `Source` **Find People**

**Inputs:**

-   **Company attributes:** Filter by company size, industry (include or exclude), and description keywords to narrow your search.
-   **Job title:** Filter by organizational level, function, or specific titles (e.g., CEO, VP). Results include synonyms, similar titles, and translated titles. For example, searching "Software Developer" returns results like "Frontend Engineer" and "Ingénieur logiciel."
    -   **Job title must contain exact:** Each result must contain at least one of your search terms, ignoring capitalization and special characters. Synonyms and similar titles are excluded. For example, "Founder/CEO" matches "ceo", but "Frontend Engineer" does not match "Software Developer."
    -   **Job title must match exactly:** Each result must match at least one search term exactly, including capitalization. Special characters are not allowed. For example, neither "Founder/CEO" nor "ceo" will match "CEO."
    -   **Exact phrase matching:** Wrap multi-word terms in quotes to search for exact phrases. For example, "Google Cloud" finds profiles with that specific expertise. Note: Special characters (#, +, !) and stopwords ('a', 'an', 'of', 'the') are removed.
-   **Experience:** Filter by current role duration, past position dates, and keywords in experience descriptions.
-   **Location:** Include or exclude specific regions, countries, or cities.
-   **Profile:** Filter by names, connection count, or follower count ranges.
-   **Certifications:** Search for specific certifications (e.g., AWS, Google Cloud).
-   **Languages:** Filter by specific languages spoken.
-   **Education:** Search for specific school names.
-   **Companies:** Find people at specific companies using an existing Clay table or a custom list. By default, this matches people who **currently** work at those companies.
-   **Exclude people:** Exclude up to 3 different sets of people from your search using Clay tables, CSVs, or manual lists. You can exclude up to 300,000 people total (100,000 per source). Exclusions require a LinkedIn URL.
-   **Past experiences:** Enable the **Include past experiences** toggle to extend your company, job title, and experience description keyword filters to also match against a person's past roles — not just their current one.
-   **Limit results:** Set a maximum number of results per search (up to 50,000 records).
-   **Limit per company:** Set the maximum number of people to return per company (up to 100). Note: the preview count shown before running the search reflects the total match universe across all companies and does not account for this limit — the actual number of imported rows will be lower.

**Outputs:**

Each result includes a **Structured Location** object in the cell details with geocoded, normalized fields — so you don't need additional AI columns to parse or reformat location data. These fields work with informal location names like "Greater Chicago Area."

-   **City**
-   **State**
-   **Region**
-   **Country**
-   **Country Iso**

## Enriching your results

After importing Find People results, use Clay's enrichments to add contact information such as work email and mobile phone numbers.

**Work email:** In your table, click `Add enrichment` and select `Work Email`. This pre-built waterfall searches multiple email providers in sequence. For full setup details, including how credits are charged across providers, see [Work Email waterfall](work-email-waterfall.md).

**Mobile phone:** To find mobile phone numbers, click `Add enrichment`, search for `Phone number`, and select the waterfall option under **Waterfalls**. The phone number waterfall cascades through multiple providers in sequence — providers that return no result are skipped at no credit cost, so you only pay when a provider finds a number. For provider recommendations by region, see [[Data test] Mobile phone providers by region](data-test-methodology-mobile-phone-region.md).

## Importing from a Sales Navigator search URL

If you have a saved Sales Navigator search and want to pull those results into Clay, use the **Find people from external search** source — not the standard Find People source described above.

1.  In a workbook, click `+ Add` at the bottom.
2.  Search for `external search`.
3.  Select **Find people from external search**.
4.  Paste your Sales Navigator people search URL (e.g., `https://www.linkedin.com/sales/search/people/...`).
5.  Optionally set a **Max Count** (default and maximum is 2,500 — this is a Sales Navigator limit).
6.  Click **Import to new table**.

**Note:** This source accepts Sales Navigator **people** search URLs only. Each imported result costs 1 Clay credit.
