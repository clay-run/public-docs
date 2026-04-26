---
title: EmailBison integration
source_url: https://university.clay.com/docs/emailbison-integration
last_synced: 2026-04-26T01:39:55.552Z
upstream_hash: d1dbac2bff69ad48ab55e495078b3efc9b552ee81d74de9038be9b6c1fc8579d
---

# EmailBison integration

Import leads into campaigns directly from Clay, ensuring accurate and efficient campaign execution.

EmailBison is a lead management platform that enables seamless synchronization of lead data between Clay and campaign interfaces.

With this integration, you can import leads into campaigns directly from Clay, ensuring accurate and efficient campaign execution.

## Enriching data with EmailBison

1.  While in a Clay table, click `Add enrichment` and search for `EmailBison`.
2.  Under `Integrations`, select one of the EmailBison options.
3.  In the modal, you'll be asked to `Select EmailBison account`.
    -   If you haven't already connected your EmailBison account, click `+ Add account` and go through authentication.

### `Action` Create or update lead

Use this action to create a new lead in EmailBison or update an existing lead if one with the same email already exists.

**Inputs**

-   **Email:** The email address of the lead (required - used as unique identifier).
-   **First name:** The first name of the lead (required).
-   **Last name:** The last name of the lead (required).
-   **Existing lead behavior:** Choose how to handle updates to existing leads (required).
    -   **PATCH:** Only update provided fields, leaving other values unchanged.
    -   **PUT:** Replace all fields with new values.
-   **Title:** The job title of the lead (optional).
-   **Company name:** The company name of the lead (optional).
-   **Notes:** Additional notes about the lead (optional).
-   **Custom variables:** Any custom variables defined in your workspace (optional).

### `Action` Find lead

Use this action to look up an existing lead in EmailBison by email address or lead ID.

**Inputs**

-   **Email:** The email address of the lead to find (optional).
-   **Lead ID:** The EmailBison lead ID to find (optional).

_Note: You must provide either email or lead ID. If both are provided, email will be prioritized._

**Output**

-   **ID:** The unique lead identifier in EmailBison.
-   **Email:** Email address.
-   **First name:** First name.
-   **Last name:** Last name.
-   **Company:** Company name.
-   **Title:** Job title.
-   **Notes:** Any notes on the lead.
-   **Status:** Lead status.
-   **Tags:** Associated tags.
-   **Created at:** When the lead was created.
-   **Updated at:** When the lead was last updated.

### `Action` Import lead to campaign

Use this action to add qualified or updated leads from Clay into a designated EmailBison campaign for targeted outreach.

**Inputs**

-   **Email:** The email address of the lead to import into the campaign.
-   **Campaign ID:** The unique identifier of the EmailBison campaign to which the lead will be added.

**Output**

-   **Success:** Lead successfully added to the EmailBison campaign.
-   **Lead ID:** The unique identifier assigned to the lead in EmailBison.
-   **Campaign ID:** Confirmation of the campaign to which the lead was added.

### `Action` Add email to blocklist

Use this action to add an email address to your workspace's blocklist to prevent sending emails to that address.

**Inputs**

-   **Email:** The email address to add to your workspace's blocklist (required).

### `Action` Remove email from blocklist

Use this action to remove an email address from your workspace's email blocklist.

**Inputs**

-   **Email address (or blocklist email ID):** The email address to remove from the blocklist, or the ID of the EmailBison email blocklist entry to remove (required).

### `Action` Add domain to blocklist

Use this action to add an entire domain to your workspace's blocklist to prevent sending emails to any address at that domain.

**Inputs**

-   **Domain:** The domain to add to your workspace's blocklist (required).

### `Action` Remove domain from blocklist

Use this action to remove a domain from your workspace's domain blocklist.

**Inputs**

-   **Domain (or blocklisted domain ID):** The domain to remove from the blocklist, or the ID of the EmailBison domain blocklist entry to remove (required).

### Run settings

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))
