---
title: Woodpecker integration
source_url: https://university.clay.com/docs/woodpecker-integration
last_synced: 2026-04-26T01:40:55.539Z
upstream_hash: a69d0a12d442f11c969ed20b6cfe620fce5a781c23f3016b58f6c658d9d7ce4e
---

# Woodpecker integration

Add prospects to your database and campaigns, enriching prospect data with comprehensive details.

Woodpecker optimizes the management of prospect information by simplifying the process of adding and updating records, ensuring data accuracy and minimizing duplicates.

With this integration, you can add prospects to your database and campaigns, enriching prospect data with comprehensive details for personalized and targeted outreach.

## **Enriching data with Woodpecker**

1.  While in a Clay table, click `Add enrichment` and search for `Woodpecker`.
2.  Under `Integrations`, select one of the Woodpecker options.
    -   If you haven’t already connected your Woodpecker, click `+ Add account` and go through authentication.

### `Action` Add prospect to database

Streamlines the process of entering and updating prospect information in Woodpecker for future outreach campaigns.

**Inputs**

-   **Email (Required):** Prospect's email address (e.g., `john.doe@example.com`)
-   **Full Name:** Prospect's full name (e.g., John Doe)
-   **Company Name:** Name of the prospect's company
-   **Company Domain:** Company website domain (e.g., `clay.com`)
-   **Person LinkedIn URL:** Prospect's LinkedIn profile URL
-   **Job Title:** Prospect's job title
-   **Mobile Number:** Prospect's phone number in international format (e.g., `+1234567890`)
-   **Address:** Prospect's street address
-   **City:** Prospect's city
-   **State:** Prospect's state/region
-   **Country:** Prospect's country
-   **Industry:** Prospect's industry
-   **Tags:** Labels to categorize the prospect (comma-separated, automatically prefixed with #)
-   **Snippets 1-15:** Custom fields for additional information

### `Action` Update prospect in database

Streamlines the process of entering and updating prospect information in Woodpecker for future outreach campaigns.

**Inputs**

-   **Email (Required):** Prospect's email address (e.g., `john.doe@example.com`)
-   **Full Name:** Prospect's full name (e.g., John Doe)
-   **Company Name:** Name of the prospect's company
-   **Company Domain:** Company website domain (e.g., `clay.com`)
-   **Person LinkedIn URL:** Prospect's LinkedIn profile URL
-   **Job Title:** Prospect's job title
-   **Mobile Number:** Prospect's phone number in international format (e.g., `+1234567890`)
-   **Address:** Prospect's street address
-   **City:** Prospect's city
-   **State:** Prospect's state/region
-   **Country:** Prospect's country
-   **Industry:** Prospect's industry
-   **Tags:** Labels to categorize the prospect (comma-separated, automatically prefixed with #)
-   **Snippets 1-15:** Custom fields for additional information

### `Action` Update prospect in campaign

Streamlines the process of adding and enriching detailed prospect data in a specific Woodpecker campaign directly from Clay.

**Inputs**

-   **Campaign ID:** Select the campaign you want to add the prospect to from the dropdown menu
-   **Email:** The prospect's email address (e.g., `john.doe@example.com`)
-   **Send after date (Optional):** Earliest contact date/time (accepts "5 days from now"or `yyyy-MM-dd` format)
-   **Full Name (Optional):** Prospect's full name (must include both first and last name)
-   **Company Name (Optional):** Prospect's company name
-   **Company Domain (Optional):** Company website domain (e.g., `clay.com`)
-   **Person LinkedIn URL (Optional):** Prospect's LinkedIn profile URL
-   **Job Title (Optional):** Prospect's job title
-   **Mobile Number (Optional):** Prospect's phone number (e.g., `+1234567890`)
-   **Address (Optional):** Prospect's address
-   **City (Optional):** Prospect's city
-   **State (Optional):** Prospect's state
-   **Country (Optional):** Prospect's country
-   **Industry (Optional):** Prospect's industry
-   **Tags (Optional):** Tags to associate with the prospect (comma-separated)
-   **Snippets (Optional):** Up to 15 custom snippets for email templates

### **Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))
