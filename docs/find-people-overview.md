---
title: Find People in Clay
description: Discover relevant contacts and LinkedIn posts using Clay's Find People and Find professional posts sources, then enrich results with work email and mobile phone waterfalls.
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
-   **Experience:** Filter by current role duration, number of positions held, and keywords in experience descriptions. The Experience section contains three sub-filters:
    -   **Months in current role:** Set a minimum and/or maximum number of months a person has been in their current position.
    -   **Number of experiences:** Set a minimum and/or maximum count of separate job entries listed on a person's LinkedIn profile. **This counts individual roles, not total years of career experience.** For example, setting Max = 2 returns people with two or fewer job entries, which is a useful proxy for early-career candidates. There is no direct "total years of experience" filter in Clay — to approximate one, combine this filter with a cap on **Months in current role**, or import results first and use a **Use AI** column to analyze each person's full work history against your criteria.
    -   **Experience description keywords:** Return only people whose experience descriptions include specific keywords (e.g., "construction", "machine learning").
-   **Location:** Include or exclude specific regions, countries, or cities.
-   **Profile:** Filter by names, connection count, or follower count ranges.
-   **Certifications:** Search for specific certifications (e.g., AWS, Google Cloud).
-   **Languages:** Filter by specific languages spoken.
-   **Education:** Search for specific school names.
-   **Companies:** Find people at specific companies using an existing Clay table or a custom list. By default, this matches people who **currently** work at those companies.
    -   **Locked after creation:** The filter type (Clay table vs. custom list) and which table is linked cannot be changed once the source exists — this is what the "Can only be changed during source creation" tooltip means. The table's row contents are not frozen, however: adding or removing rows from the linked table is reflected each time the source runs. When re-run after new companies are added, the source searches across all companies currently in the table, not just the newly added ones.
    -   **Run settings:** The source runs **Manually** by default — adding new companies to the linked table does not automatically trigger a new run. To automatically pick up new companies on a recurring basis, click the source column header in your people table, expand **Run settings**, and switch from **Manually** to **On a schedule**. Choose a frequency (Daily is most common) and click **Save schedule**. You can also click **Run now** at any time for an immediate on-demand run.
-   **Exclude people:** Exclude up to 3 different sets of people from your search using Clay tables, CSVs, or manual lists. You can exclude up to 300,000 people total (100,000 per source). Exclusions match by individual professional profile URL — each row in your exclusion table must contain a person-level profile URL. Adding a company name, domain, or company page URL to the exclusion table will **not** suppress all people from that company.

    **To exclude all people at a specific company**, use a post-import lookup instead: after importing your Find People results, add a **Lookup single row in other table** action that matches each person's company domain against your company blocklist. Set a run condition on downstream enrichments (for example, `{{Company Blocklist Lookup}} is not empty` → skip) to suppress anyone whose employer appears on your list. See [Excluding records during enrichment](finding-companies-and-people-in-clay.md#excluding-records-during-enrichment) for the full pattern.
-   **Past experiences:** Enable the **Include past experiences** toggle to extend your company, job title, and experience description keyword filters to also match against a person's past roles — not just their current one.
    -   **Incompatible filters:** This toggle cannot be combined with **Limit per company** or any **Company attributes** filter (company size, company industries, or company description keywords). Selecting them together returns an error.
    -   **May return fewer results when enabled:** Because exclude keywords apply to a person's entire work history when this toggle is on, the result count can decrease rather than increase. For example, if "Manager" is an excluded title, anyone who has ever held a role containing that word is filtered out — not just people whose current role matches.
-   **Limit results:** Set a maximum number of results per search (up to 50,000 records).
-   **Limit per company:** Set the maximum number of people to return per company (up to 100). Note: the preview count shown before running the search reflects the total match universe across all companies and does not account for this limit — the actual number of imported rows will be lower.

**Note:** If your Find People search imports only around 48–50 rows despite a much larger company list, this is a known issue: when **Limit per company** is configured, the initial import can exit early if the search preview returns fewer than 50 profiles due to how results are sampled across companies. **Workaround:** Re-open the source configuration (click the source and select **Edit**), make any minor change, and re-run — or create a new table with the same search settings. Either approach triggers the full import and returns all matching results.

**Outputs:**

Each result includes a **Structured Location** object in the cell details with geocoded, normalized fields — so you don't need additional AI columns to parse or reformat location data. These fields work with informal location names like "Greater Chicago Area."

-   **City**
-   **State**
-   **Region**
-   **Country**
-   **Country Iso**

## Enriching your results

**Note on data freshness:** Find People results come from a periodically refreshed index — not a live LinkedIn lookup at search time. A person's job title or company in the results may not reflect their most recent LinkedIn update. To get current employment data, run **Enrich Person** after importing — this fetches the live profile and returns the most up-to-date job title and company information.

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

**Note:** This source requires a Sales Navigator **people search URL** (`https://www.linkedin.com/sales/search/people/...`), not a saved lead list URL (`linkedin.com/sales/lists/people`) or a saved search URL (those containing `savedSearchId`). If you have a saved Sales Navigator lead list, recreate the equivalent filters as a fresh people search on Sales Navigator and copy that URL instead. Each imported result costs 1 Clay credit.

## Finding LinkedIn posts by keyword

To find LinkedIn posts containing a specific keyword or hashtag, use the **Find professional posts** source — a separate source from Find People that returns posts rather than people profiles.

**To create a table with Find professional posts:**

1.  In a workbook, click `+ Add` at the bottom.
2.  Search for `Find professional posts` and select it.

**Inputs:**

-   **Keyword:** A single keyword or hashtag to search for in post content (e.g., `#cvpr2026` or `GTM`). Only one keyword is supported — comma-separated lists are not valid.
-   **Companies filter (optional):** Limit results to posts that mention companies, were posted by companies, or were posted by employees of specific companies.
-   **People filter (optional):** Limit results to posts that mention or were posted by specific individuals.
-   **Sort by:** `Most recent` (default) or `Top match`.
-   **Time frame:** `Last 24 hours` or `Last week` (default).
-   **Max number of results:** Default is 100; maximum is 1,000.

**Outputs:**

Each row includes the post URL, post text, author name, author LinkedIn URL, author title, reaction counts, comment count, and share count.

**To enrich post authors:** After importing results, add an **Enrich Person** column and map it to the author LinkedIn URL. This returns full contact data — work email, company, and more — for each post author.

**To get comments, reactions, or shares on a specific post:** Click `Add enrichment`, search for **Get comments on a professional post**, **Get reactions on a professional post**, or **Get shares on a professional post**, and map **Post URL** to the post URL column from your import.

> **Important:** These actions require the original post URL — a URL containing `-activity-` in the path (e.g., `https://www.linkedin.com/posts/clay-hq_...-activity-7212099008951975937-ezPv`). Share URLs containing `-share-` are not valid and return an error. To get the original URL for any post: open the post on LinkedIn, click **•••** (three dots) at the top right of the post, and select **Copy link to post**. If the post is a repost of someone else's content, open the original underlying post first and copy its link.

## Getting people who interacted with a post

To build a table of people who liked, commented on, or shared a specific post, use the **Get interactions with professional posts** source. Each interaction is included as a separate row, and you choose how duplicate interactions are handled via the required **duplicate interaction behavior** setting:

-   **One row per person globally** (`interactor`): a given person appears at most once across all results.
-   **One row per person per post** (`post-interactor`): a given person appears at most once per post, but can appear across multiple posts.
-   **Include all interactions** (`no-dedupe`): every interaction is returned as its own row, so the same person can appear in many rows.

**To set up this source:**

1.  In a workbook, click `+ Add`.
2.  Search for `Get interactions with professional posts` and select it.
3.  Provide the post URL — either as a manual entry or by linking to a column in an existing Clay table.

**URL format requirement:** This source only accepts `activity` and `ugcPost` type post URLs. Share URLs — those containing `-share-` between the author slug and the post ID — are not valid and return an invalid-URL error. To identify the URL type: valid post URLs contain either `-activity-` or `ugcPost` in the path; share post URLs contain `-share-` and are not accepted.

To get the correct URL: open the post, click **•••** (three dots) at the top right of the post, and choose **Copy link to post**. If the post is a reshare, open the original underlying post first and copy its link from there.
