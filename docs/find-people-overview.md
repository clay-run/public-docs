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

**Outputs:**

Each result includes a **Structured Location** object in the cell details with geocoded, normalized fields — so you don't need additional AI columns to parse or reformat location data. These fields work with informal location names like "Greater Chicago Area."

-   **City**
-   **State**
-   **Region**
-   **Country**
-   **Country Iso**

## Find People from External Search

If you want to import people from a Sales Navigator People Search URL rather than searching Clay's built-in database, use the **Find People from External Search** source. This is a separate source from the regular Find People search.

### How to set it up

1.  In Sales Navigator, build your People search using the desired filters. Run the search — do **not** save it as a list or load it from your search history.
2.  Copy the People Search URL from your browser's address bar.
3.  In Clay, click **+ Add** at the bottom of a workbook.
4.  In the source search bar, type **External** and select **Find People from External Search**.
5.  Paste your Sales Navigator People Search URL into the provided field.
6.  Optionally set a result limit, then click **Save**.

### URL requirements

The URL must be a **live Sales Navigator People Search** — not a saved search, a recent search, or a saved lead list. URLs that contain `savedSearchId`, `recentSearchId`, or `/sales/lists/people` will be rejected with the error **"You must include a valid People Search URL."**

To get a valid URL: run a fresh search in Sales Navigator (do not load from recent searches or saved searches), then copy the URL directly from the address bar.

### Limits and credits

-   Up to **2,500 results** per source
-   **1 Clay credit** per person returned

The results count toward your table's 50,000-row limit.
