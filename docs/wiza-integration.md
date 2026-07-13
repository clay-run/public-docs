---
title: Wiza integration
description: Streamline contact enrichment workflows
last_synced: 2026-04-26T01:40:55.218Z
---

# Wiza integration

Streamline contact enrichment workflows

Wiza enhances contact data management by automating the discovery and validation of emails, professional profiles, and phone numbers.

With this integration, you can streamline contact enrichment workflows, reducing manual effort while enhancing the accuracy and completeness of lead information.

## **Enriching data with Wiza**

1.  While in a Clay table, click `Add enrichment` and search for `Wiza`.
2.  Under `Integrations`, select one of the Wiza options.
3.  In the modal, select or add your Wiza account.
    -   If you have your own account, click `+ Add account` and go through authentication. Otherwise, use the Clay provided key.

### `Action` Find email

Use this action to locate and verify a person's work email address using their name and company information.

**Inputs**

-   **Full Name:** The full name of the person (required with company information)
-   **Company Name:** The person's company name
-   **Company Domain:** The company's domain name
-   **Professional Profile URL:** LinkedIn profile URL (can be used instead of name/company)
-   **Email Options:** Choose from:
    -   Work Email (default)
    -   Personal Email
    -   Both

**Output**

-   Returns email addresses based on the selected options.

### `Action` Find professional profile

Use this action to discover and enrich professional profile information using contact details.

**Inputs**

-   **Email:** The email address of the person whose professional profile you want to find
-   **Full name:** The person's full name (must be used with company name)
-   **Company name:** The company where the person works
-   **Company domain (Optional):** The company's website domain for better matching accuracy

**Output**

-   **Name:** The person's full name
-   **Title:** Current job title
-   **Company:** Current company name
-   **Location:** Geographic location
-   **Company domain:** Company website domain
-   **LinkedIn profile URL:** Direct link to the person's professional profile

### `Action` Find phone number

Use this action to locate and enrich contact records with phone numbers using LinkedIn profile URLs.

**Inputs**

-   **Full Name:** The full name of the person (required with company details)
-   **Company Name:** The company name of the person
-   **Company Domain:** The company domain of the person
-   **Professional Profile URL:** The LinkedIn profile URL (e.g., `https://www.linkedin.com/in/colinparsonscom`)

**Output**

-   **Name:** The contact's full name
-   **Mobile Phone:** The contact's mobile phone number
-   **Phone Number:** Any additional phone numbers found
-   **Title:** The contact's job title
-   **Phones:** Array of all phone numbers found with additional details

### **Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

## Troubleshooting

### Wiza times out on large batches, causing waterfall fallthrough and extra credits

Wiza processes work-email lookups asynchronously. When you run many rows at once, multiple concurrent Wiza calls can queue up, causing Clay's requests to time out. In a waterfall enrichment, a timeout is treated as a failed step: Clay falls through to the next provider and charges credits, even though Wiza did not have a chance to return a result.

**To prevent unintended credit spend from Wiza timeouts:**

**Option 1 — Run Wiza in smaller batches (native integration):**

The native Wiza integration does not include a built-in rate-limit setting, so controlling how many rows run concurrently is the primary lever.

-   **Set a row limit.** Click the **rows** button in the table toolbar (e.g., **6,236/6,236 rows**) and enter a value in the **Row limit** field to cap how many rows are eligible to run at a time. See [Run progress](run-progress.md#setting-a-row-limit) for details.
-   **Run a subset of rows.** Select a range of rows by clicking the first row number and Shift-clicking the last, then right-click and choose **Run [N] rows**. This runs only those rows, leaving the rest untouched until you are ready.

**Option 2 — Split Wiza into its own column and add a run condition on downstream providers:**

Run Wiza as a standalone enrichment column instead of placing it inside a waterfall. Then add an **Only run if** condition to the next provider or waterfall in your sequence — for example, `[Wiza column] is empty` — so downstream providers only fire when Wiza genuinely returned no result. A timed-out Wiza cell shows as an error rather than as blank, so the downstream provider is skipped on timeouts and only runs when Wiza had no match. See [Conditional runs](conditional-runs.md) for setup steps.

**Option 3 — Rebuild Wiza as a custom HTTP API column:**

If you configure Wiza via an [HTTP API](http-api-integration-overview.md) column instead of the native integration, you can enable the **Custom rate limit** setting to automatically throttle how many Wiza requests Clay sends per time window. Set **Request Limit** (the maximum number of calls per window) and **Duration (in ms)** (the length of the window in milliseconds) in the **Configure** tab to match your Wiza plan's concurrency limits. This prevents timeouts without requiring manual batch management. See [HTTP API: Custom rate limit](http-api-integration-overview.md#step-7-custom-rate-limit) for details.
