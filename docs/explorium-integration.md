---
title: Explorium integration
source_url: https://university.clay.com/docs/explorium-integration
description: Access structured data from public filings, employee reviews, and social media.
last_synced: 2026-04-26T01:39:57.835Z
upstream_hash: 7a0a4d4dedfb49bdb05bf007a0a341010340a38cff969400fe5bbd1bc03a5665
---

# Explorium integration

Access structured data from public filings, employee reviews, and social media.

Explorium provides five company-level enrichments that return structured data from public filings, employee reviews, and social media. These enrichments support prospecting, segmentation, qualification, and research workflows directly in Clay.

## Enriching data with Explorium

-   While in a Clay table, click `Add enrichment` and search for `Explorium`.
-   Under `Integrations`, select one of the Explorium enrichment options.
-   In the modal, you will be asked to `Select Explorium account`.
    -   If you haven't already connected your Explorium account, click `+ Add account` and go through authentication.

### `Action` Enrich company ratings and employee sentiment

Use this action to access company ratings and employee sentiment data, including information about company culture, management quality, work-life balance, compensation satisfaction, and overall employee sentiment.

**Inputs**

**Company identifiers** (at least one required): Explorium uses a multi-step resolution strategy based on the fields you provide. The company domain is the most accurate resolution method. The more fields you provide, the more accurate the resolution will be.

-   **Company domain** (Optional): The domain of the company you are trying to enrich. Example: `clay.com`
-   **Company professional profile URL** (Optional): Company professional profile URL of the company you are trying to enrich. Example: `https://www.linkedin.com/company/grow-with-clay`
-   **Company name** (Optional): Company name of the company you are trying to enrich. Example: `Clay`
-   **Explorium ID** (Optional): Explorium ID of the company you are trying to enrich if you already have it from a previous enrichment.

**Output:** This enrichment returns ratings that cover various aspects of company culture, management quality, work-life balance, salary satisfaction, and overall employee sentiment. The information is sourced from online ratings and reviews published by current and former employees, as well as interview candidates.

**Key data points:**

-   **Company information:** Company name, location (city, region, country), address, and website
-   **Overall rating:** Overall company rating score
-   **Business outlook:** Employee sentiment about the company's business outlook (percentage)
-   **Career opportunities:** Rating for career growth opportunities
-   **CEO approval:** CEO approval rating and number of responses
-   **Compensation & benefits:** Rating for compensation and benefits packages
-   **Diversity & inclusion:** Rating for diversity and inclusion initiatives
-   **Senior management:** Rating for senior management effectiveness
-   **Work-life balance:** Rating for work-life balance
-   **Recommend to friend:** Percentage of employees who would recommend the company to a friend
-   **Review counts:** Total number of reviews and all reviews count

**Important notes:**

-   This action costs 4 credits per successful enrichment.
-   If no data is found for a company, credits are automatically refunded.
-   If the company is not found in Explorium's database, the enrichment will return an error.

### `Action` Enrich public company competitive landscape

Use this action to get insights into a company's market positioning, competitive differentiation, and key competitors sourced from publicly available financial reports, regulatory filings, and industry analysis, with links to official SEC filings such as `10-K` reports.

**Inputs**

**Company identifiers** (at least one required):

-   **Company domain:** Company website domain (e.g., `apple.com`)
-   **Company professional profile URL:** Company LinkedIn URL (e.g., `https://www.linkedin.com/company/apple`)
-   **Company name:** Full legal name of the company (e.g., `Apple Inc.`)
-   **Explorium ID:** Explorium's internal company identifier (if known from a previous enrichment)

**Output:**

-   **Key competitors:** Array of competitor company names
-   **Competitive differentiation:** Array of statements describing the company's competitive advantages and unique positioning
-   **Company name:** Official company name from SEC filings
-   **Ticker:** Stock ticker symbol (e.g., `xnas:aapl`)
-   **CIK:** Central Index Key (SEC company identifier)
-   **Form type:** Type of SEC filing (typically `10-K`)
-   **Form description:** Description of the filing type
-   **Filed at:** Date when the report was filed with the SEC
-   **Accession number:** SEC filing accession number
-   **Link to filing details:** Direct link to the detailed SEC filing page
-   **Link to HTML:** Direct link to the HTML version of the SEC filing

**Important notes:**

-   This action costs 4 credits per successful enrichment.
-   If no data is found for a company, credits are automatically refunded.

### `Action` Enrich public company strategic insights

Use this action to get in-depth information on target markets, value proposition, supplier relationships, product strategies, and sales/marketing priorities of public companies sourced from regulatory filings, earnings reports, and official company disclosures.

**Inputs**

**Company identifiers** (at least one required):

-   **Company domain:** Company website domain
-   **Company professional profile URL:** Company LinkedIn URL
-   **Company name:** Full legal name of the company
-   **Explorium ID:** Explorium's internal company identifier (if known)

**Important notes:**

-   This action costs 4 credits per successful enrichment.
-   If no data is found for a company, credits are automatically refunded.

### `Action` Enrich public company business challenges

Use this action to get insights into a company's investment history, advisory board, M&A activity, and funding rounds sourced from regulatory filings, public disclosures, and investment databases.

**Inputs**

**Company identifiers** (at least one required):

-   **Company domain:** Company website domain
-   **Company professional profile URL:** Company LinkedIn URL
-   **Company name:** Full legal name of the company
-   **Explorium ID:** Explorium's internal company identifier (if known)

**Output:** This enrichment returns business challenge categories including:

-   **Technological disruption:** Challenges related to rapid technological change and innovation requirements
-   **Company data security breach:** Risks related to cyberattacks and data breaches
-   **Company data security privacy:** Data protection and privacy compliance challenges
-   **Company competition:** Competitive pressures and market challenges
-   **Company customer adoption:** Product adoption and transition management issues
-   **Company market saturation:** Market saturation and competition in established markets
-   **Company name:** Name of the company
-   **CIK:** Central Index Key (SEC identifier)
-   **Ticker:** Stock ticker symbol
-   **Form type:** Type of SEC filing (e.g., `10-K`)
-   **Form description:** Description of the filing
-   **Accession number:** SEC filing accession number
-   **Filed at:** Date when the filing was submitted
-   **Link to HTML:** Link to the SEC filing HTML page
-   **Link to filing details:** Link to detailed SEC filing

**Important notes:**

-   This action costs 4 credits per successful enrichment.
-   If no data is found for a company, credits are automatically refunded.

### `Action` Enrich company social media metrics

Use this action to track a company's professional social media activity, engagement, and messaging trends sourced from public social media feeds.

**Inputs**

**Company identifiers** (at least one required):

-   **Company domain:** Company website domain
-   **Company professional profile URL:** Company LinkedIn URL
-   **Company name:** Full legal name of the company
-   **Explorium ID:** Explorium's internal company identifier (if known)

**Important notes:**

-   This action costs 4 credits per successful enrichment.
-   If no data is found for a company, credits are automatically refunded.

## Run settings

-   **Auto-update:** Set enrichment to refresh automatically at regular intervals.
-   **Only run if:** The enrichment will only run if conditions are met. Learn more about [conditional formulas](https://www.clay.com/university/lesson/conditional-formulas-only-run-if).
