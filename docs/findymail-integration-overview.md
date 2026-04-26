---
title: Findymail integration
source_url: https://university.clay.com/docs/findymail-integration-overview
last_synced: 2026-04-26T01:39:59.775Z
upstream_hash: 8c4aa065e619fc5923ffeff23af0a7c6999a03c5a97ad99808681fe78210364a
---

# Findymail integration

Verified B2B email data for sales outreach.

Findymail is a verified email finder and validator for B2B prospecting. Within Clay, you can use Findymail to find work emails from a name and domain, find work emails, find mobile phone numbers, and validate email addresses.

## Enriching data with Findymail

1.  While in a Clay table, click `Add enrichment` and search for `Findymail`.
2.  Under `Integrations`, select one of the Findymail actions.
3.  In the modal, you will be asked to `Select Findymail account`.
    -   If you haven't already connected your Findymail account, click `+ Add account` and enter your Findymail API key. You can find your API key at [https://app.findymail.com/user/api-tokens](https://app.findymail.com/user/api-tokens). Otherwise, use the Clay provided key.

### `Action` Find Work Email

Use this action to find a work email address for a person using their full name and company domain.

**Inputs**

-   **Full Name:** The full name of the person whose work email you are trying to find.
-   **Company Domain:** The company domain of the person whose work email you are trying to find (e.g., `clay.com`).

**Outputs**

-   **Email:** The work email address found for the person.
-   **Status:** The validity status of the email (e.g., `valid`).

**Pricing:** 2 credits per enriched cell with Clay-managed account.

### `Action` Find Work Email from Profile URL

Use this action to find a work email address for a person using their LinkedIn profile URL.

**Inputs**

-   **Personal Profile URL:** The LinkedIn URL of the person you want to find the work email for (e.g., `https://linkedin.com/in/examplename`).

**Outputs**

-   **Email:** The work email address found for the person.
-   **Status:** The validity status of the email (e.g., `valid`).

**Pricing:** 2 credits per enriched cell with Clay-managed account.

### `Action` Find Mobile Phone

Use this action to retrieve a mobile phone number associated with a LinkedIn profile URL.

**Inputs**

-   **Professional URL:** The LinkedIn profile URL of the person whose phone number you want to find (e.g., `https://linkedin.com/in/examplename`).

**Outputs**

-   **Mobile Phone:** The mobile phone number associated with the LinkedIn profile (e.g., `+19199463022`).

**Pricing:** 9 credits per enriched cell with Clay-managed account.

### `Action` Validate Email

Use this action to verify whether an email address is valid using Findymail.

**Inputs**

-   **Email:** The email address to validate.

**Outputs**

-   **Email:** The validated email address.
-   **Verified:** Whether the email address is valid (`true` or `false`).

**Pricing:** 1 credit per enriched cell with Clay-managed account.

### Run settings

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))
