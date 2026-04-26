---
title: Find People in Clay
source_url: https://university.clay.com/docs/find-people-overview
last_synced: 2026-04-26T01:39:58.803Z
upstream_hash: 38622f4eb47a29257c2c283ccf0bce72123a4902190c52961bd8a1c1e45b44d8
---

# Find People in Clay

Discover relevant contacts matching your criteria within Clay's database.

The `Find People` source helps you search for people using criteria like job title, company, location, and experience.

This tool is ideal for building targeted sales prospect lists, identifying potential hires, and conducting market research.

**Note:** You can get up to 500 results per cell by reducing the data you're requesting. Click the column name and select **Edit column → Reduce Data for More Results**.

## **Creating a table with Find People**

**From the Find leads page (recommended for new searches):**

1.  Click **Find leads** in the left sidebar.
2.  On the **People** tab, click the **Clay** source card.

**From within a workbook:**

1.  In a workbook, click `+ Add` at the bottom.
2.  Search for `Find People`.

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
-   **Limit per company:** Set the maximum number of people to return per company (up to 100).
