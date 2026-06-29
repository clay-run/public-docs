---
title: Clay Lookalikes
description: Find companies or people similar to a seed list using Clay's native lookalike engine, powered by AI embeddings.
last_synced: 2026-06-09T00:00:00.000Z
---

# Clay Lookalikes

Find companies or people similar to a seed list using Clay's native lookalike engine.

Clay Lookalikes is a first-party Clay feature that uses AI-powered embeddings to find companies and people that closely match your best customers, partners, or ICP — without manually specifying filters. It is the recommended replacement for Ocean.io's lookalike features, [which have been removed from Clay](#migrating-from-ocean-io).

## Accessing Clay Lookalikes

The **Company Lookalikes source** (table-builder) can be accessed two ways:

-   **Home → Find leads → Lookalikes** — select the **Lookalikes** card from the quick-start grid on the Find Leads homepage.
-   **Find Companies page** — open the Find Companies setup panel and switch to **Find lookalikes** using the mode dropdown in the filter panel header.

**People Lookalikes** is available both as a standalone **Find People Lookalikes source** (table-builder, powered by Lusha and runnable on Clay credits without a Lusha API key) and as an in-table enrichment. See [`Action` Find People Lookalikes](#action-find-people-lookalikes) below.

## `Source` Find Company Lookalikes (Clustered)

Build a new table of lookalike companies from a seed list. Results are organized into clusters that you can review, refine, and edit before importing.

**To create a table with company lookalikes:**

1.  In a workbook, click `+ Add` at the bottom.
2.  Search for `Lookalikes` and select **Find lookalike companies (grouped)**, or navigate to **Home → Find leads → Lookalikes**.
3.  Choose your seed input:
    -   **Table** — a Clay table of companies (up to 15,000 companies)
    -   **Audience** — a Clay Audiences segment (up to 15,000 companies)
    -   **List of URLs** — enter company domains or LinkedIn company URLs manually
4.  Review the generated lookalike groups. Each group represents a cluster of similar companies. Use Sculptor to edit a group's filters — you can add or remove industries, company sizes, countries, and description keywords.
5.  Click **Continue** to import results into a new Clay table.

**Credits:**

| Seed type | Modern plans | Legacy plans |
|---|---|---|
| Table or Audience | 2 credits / result | 3 credits / result |
| List of URLs | 1 credit / result | 1.5 credits / result |

## `Action` Find Company Lookalikes

Add a column to an existing table to enrich each row with companies similar to that row's company.

1.  In a Clay table, click `Add enrichment` and search for `Find Company Lookalikes`.
2.  Map the required input to a company domain or LinkedIn URL column.
3.  Optionally configure additional filters (industry, company size, keywords, etc.).
4.  Run the enrichment.

**Credits:** 1 credit per result returned.

## `Action` Find People Lookalikes

Find people similar to a seed person. In addition to the standalone **Find People Lookalikes source** (table-builder, which accepts 5–100 seed LinkedIn URLs or emails and can run on Clay credits without a Lusha API key), this is also available as an in-table enrichment. The enrichment identifies companies similar to the seed person's employer and then finds people with matching titles and seniority levels at those lookalike companies.

1.  In a Clay table, click `Add enrichment` and search for `Find People Lookalikes`.
2.  Map **Professional profile URL** to the LinkedIn URL column for your seed person. You can alternatively provide an **Email** if no LinkedIn URL is available.
3.  Configure optional filters:
    -   **Seniorities** — seniority levels to include (auto-derived from the seed person if not provided)
    -   **Job title keywords** — keywords to match in the person's current job title
    -   **Use smart job title expansion** — when enabled, expands keywords with LLM-generated synonyms such as "VP of Eng" → "Vice President of Engineering" (on by default)
    -   **Countries** — filter people by country of location
    -   **Lookalike company domain** / **Lookalike company LinkedIn URLs** — override the seed person's employer with specific domains or LinkedIn URLs to find people at companies similar to a different target
    -   **Domains to include / exclude** — force-include or skip people from specific company domains (the seed person's company is always excluded automatically)
    -   **Company primary countries**, **Company sizes**, **Company industries** — narrow the universe of lookalike companies considered
    -   **Maximum number of lookalikes** — total number of people to return (default 25, max 50)
    -   **Maximum lookalikes per company** — cap per lookalike company (default 5, max 50)
4.  Run the enrichment.

**Output:** An array of matching people, each with name, LinkedIn URL, job title, company domain, seniority levels, and country.

**Credits:** 1 credit per result returned.

## Migrating from Ocean.io

Clay Lookalikes replaces Ocean.io's lookalike enrichments and sources. Ocean.io's lookalike features have been removed from Clay — see [Ocean.io integration](ocean-io-integration-overview.md) for migration guidance.
