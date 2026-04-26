---
title: Lusha integration
source_url: https://university.clay.com/docs/lusha-integration
description: Verify contact and company data, including work emails, phone
  numbers, and buying signals.
last_synced: 2026-04-26T01:40:18.523Z
upstream_hash: 4d57e29e17e574487d524b27f5e62c320ec1dfb56f20845da248797b4d353ae6
---

# Lusha integration

Verify contact and company data, including work emails, phone numbers, and buying signals.

Lusha is a B2B sales intelligence platform that provides verified contact and company data, including work emails, phone numbers, and buying signals.

With Clay's Lusha integration, you can enrich person and company records, detect career-change and company-level signals, and build targeted prospect lists using lookalike prospecting.

## **Creating a table with Lusha**

1.  In a workbook, click `+ Add` at the bottom.
2.  Search for `Lusha` and select from the results.
3.  In the modal, you will be asked to `Select Lusha account`.
    -   If you haven't already connected your Lusha account, click `+ Add account` and enter your Lusha API key. You can find your API key in your Lusha account under `Settings → API`.
    -   **Note:** Lusha sources (lookalike searches) can be run using Clay credits without requiring a Lusha API key.

### `Source` Find company lookalikes

Find similar companies based on a list of seed companies using Lusha.

**Inputs**

-   **Company domains:** Comma-separated list of company domains to use as seeds (e.g., `sap.com, oracle.com`). Required if Company professional profile URLs is not provided. Total unique company identifiers across both fields must be between 5 and 100.
-   **Company professional profile URLs:** Comma-separated list of company LinkedIn URLs (e.g., `https://www.linkedin.com/company/sap`). Required if Company domains is not provided.
-   **Company domains to exclude** (Optional): Domains to exclude from results. Maximum 500 unique exclusions.
-   **Company professional profile URLs to exclude** (Optional): Company LinkedIn URLs to exclude from results. Maximum 500 unique exclusions.
-   **Max results** (Optional): Maximum number of lookalike companies to return. Defaults to 5,000.

**Outputs**

-   **Company name:** The lookalike company's name.
-   **Company domain:** The company's domain.
-   **Company LinkedIn URL:** The company's LinkedIn profile URL.
-   **Employee count:** The number of employees at the company.
-   **Industry:** The company's industry.
-   **Location:** The company's country, state, and city.

### `Source` Find people lookalikes

Start with a list of seed contacts and find similar people aligned by job title, seniority, and company context.

**Inputs**

-   **Professional profile URLs:** Comma-separated list of LinkedIn URLs of seed contacts (e.g., `https://www.linkedin.com/in/john-doe`). Required if Emails is not provided. Total unique personal identifiers across both fields must be between 5 and 100. Best practice is to provide 10 or more.
-   **Emails:** Comma-separated list of seed contact email addresses. Required if Professional profile URLs is not provided.
-   **Professional profile URLs to exclude** (Optional): LinkedIn URLs to exclude from results. Maximum 500 unique exclusions.
-   **Emails to exclude** (Optional): Email addresses to exclude from results. Maximum 500 unique exclusions.
-   **Max results** (Optional): Maximum number of lookalike people to return. Defaults to 5,000.

**Outputs**

-   **ID:** Lusha's internal identifier for the person.
-   **First name:** The person's first name.
-   **Last name:** The person's last name.
-   **Social links → LinkedIn:** The person's LinkedIn profile URL.
-   **Company:** The person's employer, including company ID, name, and domain.
-   **Job title:** The person's title, department(s), and seniority level.
-   **Location:** The person's country, state, and city.

## **Enriching data with Lusha**

1.  While in a Clay table, click `Add enrichment` and search for `Lusha`.
2.  Under `Integrations`, select one of the Lusha options.
3.  In the modal, you will be asked to `Select Lusha account`.
    -   If you haven't already connected your Lusha account, click `+ Add account` and enter your Lusha API key.
    -   **Note:** All Lusha actions except for **Enrich person** can be run using Clay credits without requiring a Lusha API key. Only **Enrich person** requires you to connect your own Lusha account.

### `Action` Enrich person

Get key data about a person given a professional profile URL, email, or full name combined with a company name or domain.

**Inputs**

**Required (one of the following combinations):**

-   **Professional Profile URL:** The person's LinkedIn URL (e.g., `https://www.linkedin.com/in/john-doe`).
-   **Email:** The person's email address.
-   **Full Name + Company Name:** The person's full name paired with the name of the company they work at.
-   **Full Name + Company Domain:** The person's full name paired with the company's domain (e.g., `clay.com`).

**Optional:**

-   **Include Email:** Returns the person's work email. Consumes 1 Lusha Unified Credit from your Lusha account. Defaults to off.
-   **Include Phone:** Returns the person's phone number. Consumes 5 Lusha Unified Credits from your Lusha account. Defaults to off.
-   **Partial Profile:** Returns basic profile data even when no email or phone is found. Defaults to on.

**Outputs**

-   **First Name:** The person's first name.
-   **Last Name:** The person's last name.
-   **Full Name:** The person's full name.
-   **Person ID:** Lusha's internal identifier for the person.
-   **Company ID:** Lusha's internal identifier for the person's current company.
-   **Job Title:** The person's current title, department(s), and seniority level.
-   **Job Start Date:** The date the person started their current role.
-   **Previous Job:** The person's prior employer, including company name, domain, title, and seniority.
-   **Social Links:** The person's LinkedIn profile URL.
-   **Update Date:** The date this record was last updated in Lusha's database.
-   **Company:** The person's current employer, including name, description, domains, homepage URL, location (city, state, country), company size range, revenue range, and logo URL.

### `Action` Enrich company

Get firmographic data about a company using its name or domain.

**Inputs**

**Required (one of the following):**

-   **Company Name:** The name of the company to enrich (e.g., `Intercom`). Required if Company Domain is not provided.
-   **Company Domain:** The company's domain (e.g., `intercom.com`). Required if Company Name is not provided.

**Outputs**

-   **Name:** The company's name.
-   **Domain:** The company's domain.
-   **Description:** A brief description of the company.
-   **Employees:** The company's employee count range (e.g., `501 - 1000`).
-   **Founded:** The company's founding date.
-   **Logo:** URL of the company's logo.
-   **Website:** The company's website URL.
-   **Main Industry:** The company's primary industry.
-   **Categories:** A list of industry categories associated with the company.
-   **Address:** The company's full address string.
-   **Location:** The company's city, state, state code, country, and full location string.
-   **Social:**
    -   LinkedIn URL: The company's LinkedIn profile URL.
    -   Crunchbase URL: The company's Crunchbase profile URL.

### `Action` Enrich person signals

Search for contact-level signals — such as promotions or company changes — for a specific person.

**Inputs**

**Required:**

-   **Signal Type:** The type of signal to search for. Options are dynamically loaded from your Lusha account and include `All Signals`, `Promotion`, and `Company Change`.

**Required (one of the following combinations, paired with Signal Type):**

-   **Professional Profile URL:** The person's LinkedIn URL.
-   **Email:** The person's email address.
-   **Full Name + Company Name:** The person's full name and company name.
-   **Full Name + Company Domain:** The person's full name and company domain.

**Outputs**

-   **Contacts → Contact → Person ID:** The Lusha ID of the contact associated with the signal.
-   **Signal Date:** The date the signal event occurred.
-   **End Date:** The end date of the signal window returned.

### `Action` Enrich company headcount growth

Search for a company's headcount growth over a specified time period using its domain or company name. Costs 8 Clay credits per run, refunded if no data is found.

**Inputs**

**Required (one of the following):**

-   **Company Name:** The name of the company (e.g., `Clay`). Required if Company Domain is not provided.
-   **Company Domain:** The company's domain (e.g., `clay.com`). Required if Company Name is not provided.

**Optional:**

-   **Start date:** The beginning of the time window to analyze. For best results, do not go shorter than the past month. Maximum lookback is 6 months, which is also the default.

**Outputs**

-   **Headcount Growth:** An array of headcount growth signals, each containing:
    -   Company ID: Lusha's internal identifier for the company.
    -   Signal Type: The type of headcount signal detected.
    -   Score: The relative strength of the signal (e.g., `low`, `medium`, `high`).
    -   Signal Date: The date the signal was detected.
    -   Historical Avg: The historical average value for this signal type.
    -   New Value: The current value of the headcount metric.
    -   Old Value: The previous value of the headcount metric.

### `Action` Enrich company jobs growth

Search for a company's job posting growth over a specified time period using its domain or company name.

**Inputs**

**Required (one of the following):**

-   **Company Name:** The name of the company (e.g., `Clay`). Required if Company Domain is not provided.
-   **Company Domain:** The company's domain (e.g., `clay.com`). Required if Company Name is not provided.

**Optional:**

-   **Start date:** The beginning of the time window to analyze. For best results, do not go shorter than the past month. Maximum lookback is 6 months, which is also the default.

**Outputs**

-   **New Jobs Open:** An array of job growth signals, each containing:
    -   Company ID: Lusha's internal identifier for the company.
    -   Signal Type: The type of job signal detected (e.g., `new_jobs_count`).
    -   Score: The relative strength of the signal (e.g., `low`, `medium`, `high`).
    -   Signal Date: The date the signal was detected.
    -   Historical Avg: The historical average number of open jobs for this company.
    -   New Value: The current number of open jobs.
    -   Old Value: The previous number of open jobs.

### `Action` Enrich company news

Search for company-level news signals — such as funding rounds, acquisitions, or leadership changes — using a company's domain or name.

**Inputs**

**Required (one of the following):**

-   **Company Name:** The name of the company (e.g., `Clay`). Required if Company Domain is not provided.
-   **Company Domain:** The company's domain (e.g., `clay.com`). Required if Company Name is not provided.

**Optional:**

-   **Start date:** The beginning of the news window. Defaults to 6 months ago. Maximum lookback is 6 months.

**Outputs**

-   **News:** An array of news signals, each containing:
    -   Company ID: Lusha's internal identifier for the company.
    -   Event Type: The type of news event (e.g., `receives investment`).
    -   Event Category: The broader category of the event (e.g., `Financial Growth`).
    -   Event Effective Date: The date the event occurred.
    -   Event Summary: A short summary of the event.
    -   Article Sentence: A single headline sentence from the source article.
    -   Article Title: The full title of the source article.
    -   Article URL: A link to the source article.
    -   Article Published Date: The date the article was published.

### **Run settings**

-   **Auto-update:** Recommended for signal-based workflows where you want Clay to re-check for new signals or updated contact data on a recurring basis.
-   **Only run if:** The enrichment will only run when a specified condition is met. ([Learn more about conditional formulas here.](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

## **FAQs**

**Can I use multiple types of inputs to find company or person lookalikes?**

Yes! Both `Find company lookalikes` and `Find people lookalikes` support combining multiple types of inputs, whether domains, professional profile URLs, or emails. When finding person lookalikes using first name and last name, you must also include a company domain or company name to help match the correct contact.

**What happens if I toggle on additional datapoints in Enrich Person?**

Turning on additional data points, like email and phone, will consume Lusha Unified Credits from your Lusha account. Emails deduct 1 credit per contact, while phone numbers deduct 5 credits per contact.

**Are Lusha's signals actions always-on monitors?**

No. Lusha's signals actions (`Enrich person signals`, `Enrich company headcount growth`, `Enrich company jobs growth`, and `Enrich company news`) are retroactive lookups, not always-on monitors like Clay's native Signals. These actions check for events that occurred within a specified lookback window, but they won't notify you of future events as they happen.
