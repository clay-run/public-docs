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

### `Action` Find personal email

Use the Wiza **Find personal email** action to find a person's personal email address. Wiza needs enough information to identify the person, so the enrichment panel groups the inputs under **Personal identifiers** and asks for one of these input combinations:

-   **Professional profile URL** on its own, or
-   **Full name** + **Company name**, or
-   **Full name** + **Company domain**

**Inputs**

-   **Professional profile URL:** A link to the person's professional social profile. Can be used on its own instead of name and company.
-   **Full name:** The person's full name. Must be paired with a company name or a company domain.
-   **Company name:** The person's company name.
-   **Company domain:** The company's website domain. A full website URL such as `https://www.example.com` also works: Wiza's Find personal email action strips the `https://` and `www.` parts and uses the bare domain (`example.com`).

**Output**

-   Returns the personal email addresses Wiza found for the person, along with details such as name, company, and company domain. If Wiza finds no email, the cell shows **No email found**.

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

### My Wiza column shows "Awaiting Callback" — is this normal?

Yes — **Awaiting Callback** is the expected status while Wiza processes your email lookup. Wiza delivers results asynchronously: when Clay triggers a lookup, Wiza processes it in the background and sends the results back to Clay via a webhook. Your column stays in **Awaiting Callback** until that callback arrives, which typically takes a few minutes. This status does not indicate downtime.

If a cell has been in **Awaiting Callback** for more than 5 minutes, Clay's timeout has likely elapsed and the cell will have moved to an error state. To retry, re-run those rows from your table: right-click the affected cells in the Wiza column and choose **Run selected rows** to dispatch fresh lookups.

### Can I run Wiza Find personal email with only a full name and a website domain?

Yes. You don't need to fill every input in the Wiza **Find personal email** enrichment. A **Full name** column plus a **Company domain** column is one of the three accepted input combinations, so once both are mapped you can save the enrichment and run it. The other combinations are **Professional profile URL** on its own, or **Full name** + **Company name**. Your website domain column can contain full URLs (for example, `https://www.example.com`); Wiza uses the bare domain.

Things to know before you run it:

-   **Other columns aren't used.** Wiza Find personal email only accepts four inputs: Professional profile URL, Full name, Company name, and Company domain. Extra columns such as location, job title, or work environment are not sent to Wiza and won't improve personal email results.
-   **Adding a professional profile URL can improve matches.** If you only have names and a domain, you can first add a [Use AI](use-ai-integration-overview.md) column that looks up each person's professional profile URL from the information in your table. Then map that column to **Professional profile URL**.
-   **No email found isn't charged.** When Wiza returns no email, the cell shows **No email found** and the credits for that row are refunded.
-   **Rows missing a valid combination fail without charge.** If a row has no professional profile URL and is missing either the full name or both the company name and company domain, the Wiza cell errors with "You must include a professional profile URL or a full name and company name or domain." Credits for that row are refunded.
-   **Test on a few rows first.** Right-click the Wiza column header and choose **Run column** → **Choose number of rows to run** to check results on a handful of rows before running the whole table.

### Wiza times out on large batches, causing waterfall fallthrough and extra credits

Wiza processes work-email lookups asynchronously, which can take several minutes per lookup — Clay waits up to 5 minutes for a Wiza response before timing out. When you run many rows at once, multiple concurrent Wiza lookups can queue up and exhaust the concurrency limit on your Wiza API key, causing requests to stall and time out. In a waterfall enrichment, a timed-out step is treated as a non-result: Clay falls through to the next provider in the sequence and charges that provider's credits — even though Wiza did not have a chance to return a genuine match. Wiza's own credits are not consumed on timeout.

**To prevent unintended credit spend from Wiza timeouts:**

**Option 1 — Run Wiza in smaller batches (native integration):**

The native Wiza integration does not include a built-in rate-limit setting, so controlling how many rows run concurrently is the primary lever. Several approaches:

-   **Right-click the Wiza column header** and choose **Run column** → **Choose number of rows to run**, then enter how many rows to process at once. Starting with a small number lets you stay within your API key's concurrency limit.
-   **Set a row limit.** Click the **rows** button in the table toolbar (e.g., **6,236/6,236 rows**) and enter a value in the **Row limit** field to cap how many rows are eligible to run at a time. See [Run progress](run-progress.md#setting-a-row-limit) for details.
-   **Run a subset of rows.** Select a range of rows by clicking the first row number and Shift-clicking the last, then right-click and choose **Run [N] rows**. This runs only those rows, leaving the rest untouched until you are ready.

**Option 2 — Split Wiza into its own column and add a run condition on downstream providers:**

Run Wiza as a standalone enrichment column instead of placing it inside a waterfall. Then add an **Only run if** condition to the next provider or waterfall in your sequence — for example, `[Wiza column] is empty` — so downstream providers only fire when Wiza genuinely returned no result. A timed-out Wiza cell shows as an error rather than as blank, so the downstream provider is skipped on timeouts and only runs when Wiza had no match. See [Conditional runs](conditional-runs.md) for setup steps.

**Option 3 — Rebuild Wiza as a custom HTTP API column:**

If you configure Wiza via an [HTTP API](http-api-integration-overview.md) column instead of the native integration, you can enable the **Custom rate limit** setting to automatically throttle how many Wiza requests Clay sends per time window. Set **Request Limit** (the maximum number of calls per window) and **Duration (in ms)** (the length of the window in milliseconds) in the **Configure** tab to match your Wiza plan's concurrency limits. This prevents timeouts without requiring manual batch management. See [HTTP API: Custom rate limit](http-api-integration-overview.md#step-7-custom-rate-limit) for details.
