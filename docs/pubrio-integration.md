---
title: Pubrio integration
description: Find companies, identify key contacts, find phone numbers, analyze
  tech stacks, and discover job openings.
last_synced: 2026-04-26T01:40:30.939Z
---

# Pubrio integration

Find companies, identify key contacts, find phone numbers, analyze tech stacks, and discover job openings.

Pubrio enables efficient identification and contact extraction of key sales and recruiting leads by automating the search and enrichment of personnel information and company tech stacks.

With this integration, you can find companies based on firmographics, technology usage, hiring signals, news coverage, advertising activity, and cloud footprint; identify key contacts at those companies; find phone numbers; analyze tech stacks; and discover job openings to streamline outreach and analysis processes.

## **Finding companies with Pubrio**

Use the **Find companies with Pubrio** source to populate a Clay table with companies matching your filter criteria. This is a **source** — it adds new rows to your table rather than enriching existing ones. To use it, click **Add source** in a Clay table (or select it when creating a new table), then search for and select **Find companies with Pubrio**.

At least one filter is required. The source returns up to 12,500 companies per search; the default limit is 500.

**Cost:** 3 credits per company returned. Successful searches that return no results are still billed.

**Filters**

Filters are organized into the following groups. At least one filter from any group must be set:

-   **Company** — Company name (partial match), company domains, company professional profile URLs, or company search IDs returned by other Pubrio actions.
-   **Location** — Filter by HQ country (include or exclude) and by city or region (include or exclude).
-   **Industry and technology** — Filter by industry, industry category, industry sub-category, technology, technology category, or company keywords. Unrecognized terms are ignored by Pubrio and do not cause an error.
-   **Firmographics** — Filter by employee headcount band, estimated annual revenue in USD, founded year range, or social media presence (LinkedIn, Twitter/X, Facebook, Instagram, TikTok, GitHub, Wantedly, RocketPunch).
-   **Hiring** — Filter by job posting country (include or exclude), job title (similar titles also match — "software engineer" returns "senior software engineer"), or job posted date range.
-   **News** — Filter by news category or news publication date range.
-   **Advertising** — Filter by ad platform (LinkedIn, Meta, Google, TikTok, Apple), Meta ad surface, ad format, ad status, ad search terms, ad headline keywords, ad target countries, date ranges (ad start, end, and active dates), and volume metrics (active ads, running ads, total ads, platform count, format count, estimated impressions).
-   **Advertising in a specific country** — Scope advertising filters to a single country. Adds per-country rank, percentile, volume score, and impression metrics, along with first/last seen dates for ads in that country.
-   **Cloud footprint** — Filter by cloud or hosting provider (include, exclude, or primary provider only), cloud region, city, and country. Includes metrics such as host count, server count, and provider count, as well as first/last seen dates. Enable **Cross-border infrastructure only** to limit results to companies running infrastructure outside their home market.
-   **Cloud footprint in a specific country** — Scope cloud footprint filters to a single country. Adds per-country host count, server count, region count, city count, and first/last seen dates.

**Results options**

-   **Require all values for** — By default, each filter matches any value you entered. Use this option to switch selected filters to "match all values" logic (e.g., require a company to use every listed technology rather than any one of them).
-   **Sort by** — Order results by relevance, employee count, founded year, or advertising rank in a country. Advertising rank requires the **Ad activity country** filter to be set.
-   **Sort descending** — Reverse the sort order. Not supported when sorting by relevance (Pubrio serves relevance results in ascending order only).
-   **Number of companies** — How many companies to import. Defaults to 500; maximum is 12,500 per search.

**Output**

Each company row includes:

-   **Identity** — Company name, domain, company URL, company URL active status, LinkedIn URL, LinkedIn handle, LinkedIn company ID, company search ID
-   **Profile** — Industry, location, country, country code, employee count (number), employee count range (text), founded year, company ranking, specialties (list), company keywords (list)
-   **Social links** — Twitter/X, Facebook, Instagram, YouTube, TikTok, GitHub, Crunchbase, Wantedly, and RocketPunch profile URLs

## **Enriching data with Pubrio**

1.  While in a Clay table, click `Add enrichment` and search for `Pubrio`.
2.  Under `Integrations`, select one of the Pubrio options.

### `Action` Find people at company

Search for and identify key contacts at target companies based on role, department, and location filters to build targeted outreach lists.

**Inputs**

-   **Company domain:** The website domain of the company to search within (e.g., `clay.com`)
-   **Company professional profile URL:** (e.g., `https://www.linkedin.com/company/grow-with-clay/`)

_Note: Either company domain or company professional profile URL is required._

**Optional Filters**

-   **Job title:** A comma-separated list of job titles (e.g., "Software Engineer, Product Manager")
-   **Management level:** Filter by management level of the contacts
-   **Department title:** Filter by specific department names
-   **Department function:** Filter by department functions
-   **Company size:** Filter by company size ranges
-   **People locations:** Filter by contact locations
-   **Company locations:** Filter by company locations

**Output**

-   **List of matching contacts (up to 25) with details:**
-   Name and title
-   Company information
-   Department and function
-   Location
-   Professional profile URL (when available)
-   **Total number of people found**
-   **Total number of people returned** (limited to 25 per request)

### `Action` Find phone number (APAC)

The Find phone number action enriches LinkedIn profiles with phone numbers to support efficient and direct outreach.

**Inputs**

-   **Professional profile URL (Required):** The LinkedIn profile URL to find the phone number for. Must be a valid LinkedIn URL in the format `https://www.linkedin.com/in/john-doe-1234567890/`.

**Output**

-   **LinkedIn URL:** The validated LinkedIn profile URL
-   **LinkedIn name:** The LinkedIn profile name in slug format
-   **Phones:** Array of phone number details including:
-   **Value:** The phone number in E.164 format (e.g., `+16468089010`)
-   **Type:** The type of phone number
-   **Status:** Verification status of the phone number (e.g., `Verified`)

### `Action` Enrich company tech stack

Identifies and retrieves technologies used on a company's website by analyzing their domain or professional profile.

**Inputs**

-   **Company domain:** The domain of the company to find the tech stack for. (Required if profile URL not provided)
-   **Company professional profile URL:** The company professional profile URL to find the tech stack for. (Required if domain not provided)

**Output**

-   **Category ID:** Numeric identifier for the technology category
-   **Technologies:** Array of technologies found, including:
-   **Icon:** Technology's icon file name
-   **Name:** Technology name
-   **Tag ID:** Numeric identifier for the technology
-   **Version:** Version number of the technology (if available)
-   **Website:** URL of the technology provider
-   **Location:** Where the technology was detected

### `Action` Find open jobs at company

Find job listings posted by companies using their website domain or professional profile URL, returning up to 25 matching positions.

**Inputs**

-   **Company domain (Optional):** The domain of the company to find jobs for (e.g., `microsoft.com`). One of domain or company professional profile URL is required.
-   **Company professional profile URL (Optional):** The company's professional profile URL. One of domain or company professional profile URL is required.
-   **Job title (Optional):** A comma-separated list of job titles to search for (e.g., "Software Engineer, Product Manager")
-   **Post keywords (Optional):** Words to filter the results by (e.g., "Python, React")
-   **Job locations (Optional):** The locations where the jobs are based
-   **Company headquarters locations (Optional):** Filter by company headquarters location
-   **Date job posted after (Optional):** Filter jobs posted on or after a specific date (e.g., "5 days ago"or "2022-07-31")
-   **Date job posted before (Optional):** Filter jobs posted on or before a specific date (e.g., "5 days ago"or "2022-07-31")

**Output**

-   List of jobs matching the search criteria
-   Total number of jobs found
-   Total number of jobs returned (maximum 25)
-   Job title
-   Company information
-   Location
-   Posting date
-   Job description
-   Other relevant metadata

### **Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))
