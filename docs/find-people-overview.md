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
-   **Companies:** Find people at specific companies using an existing Clay table or a custom list.
-   **Exclude people:** Exclude up to 3 different sets of people from your search using Clay tables, CSVs, or manual lists. You can exclude up to 300,000 people total (100,000 per source). Exclusions require a LinkedIn URL.
-   **Past experiences:** Toggle to include past experiences in your search.
-   **Limit results:** Set a maximum number of results per search (up to 50,000 records).
-   **Limit per company:** Set the maximum number of people to return per company (up to 100). Note: the preview count shown before running the search reflects the total match universe across all companies and does not account for this limit — the actual number of imported rows will be lower.

## Getting phone numbers and emails from your results

Once Find People returns a list of contacts, you can enrich each row with contact information using Clay's pre-built waterfall enrichments — the same type of contact lookup available in dedicated tools like Lusha.

**Work email:** Click `Add enrichment` → search for `Work Email` → select it under **Waterfalls**. The waterfall cascades through multiple email providers in sequence and stops as soon as a valid result is found. Credits are only charged when an email is successfully returned.

**Mobile phone number:** Click `Add enrichment` → search for `Mobile Phone` → select the waterfall matching your target region under **Waterfalls**:

-   **Mobile Phone (US and Canada)**
-   **Mobile Phone (EMEA)**
-   **Mobile Phone (APAC)**
-   **Mobile Phone (Global)**

Credits are only charged when a number is found.

Both waterfalls are pay-per-result, so rows where no contact information is found do not consume credits. Clay's [templates library](https://www.clay.com/templates) includes prebuilt tables that combine Find People with phone and email enrichment as a ready-made starting point.
