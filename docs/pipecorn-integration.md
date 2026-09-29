---
title: Pipecorn integration
description: Find verified work emails and mobile phone numbers with Pipecorn, a waterfall of 20+ underlying data sources with especially strong European coverage.
last_synced: 2026-09-29T00:00:00.000Z
---

# Pipecorn integration

Find verified work emails and mobile phone numbers with Pipecorn, a waterfall of 20+ underlying data sources with especially strong European coverage.

Pipecorn is a contact data enrichment provider that aggregates results across 20+ underlying data sources. It provides especially strong coverage for European contacts. With this integration you can find verified work emails and mobile phone numbers.

## Using Pipecorn in Clay

1.  While in a Clay table, click `Add enrichment` and search for `Pipecorn`.
2.  Under `Integrations`, select one of the Pipecorn actions.
3.  In the modal, you will be asked to `Select Pipecorn account`.
    -   You can use the Clay-managed Pipecorn account, or bring your own key.
    -   To bring your own, click `+ Add account` and enter your Pipecorn API key.

### `Action` Find work email

Find a verified work email address for a person from their name and company domain, company name, or professional profile URL.

**Inputs**

-   **First name (Required):** Person's first name.
-   **Last name (Required):** Person's last name.
-   At least one of the following company identifiers is required:
    -   **Company domain** — e.g. `clay.com`
    -   **Company name**
    -   **Professional profile URL** — e.g. `https://www.linkedin.com/in/johndoe`

### `Action` Find mobile phone

Find a verified mobile phone number for a person from their professional profile URL.

**Inputs**

-   **Professional profile URL (Required):** Person's professional profile URL, e.g. `https://www.linkedin.com/in/johndoe`.
-   **First name (Optional):** Improves match accuracy.
-   **Last name (Optional):** Improves match accuracy.
-   **Company domain (Optional):** Improves match accuracy.
