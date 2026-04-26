---
title: Fullenrich integration
source_url: https://university.clay.com/docs/fullenrich-integration-overview
description: B2B contact enrichment for emails and phone numbers.
last_synced: 2026-04-26T01:40:01.449Z
upstream_hash: 81af6b15a5b7a7f53cca3ec6dc61e76b2b0679b39f6a259e73b0c7553c329115
---

# Fullenrich integration

B2B contact enrichment for emails and phone numbers.

FullEnrich enables you to obtain verified contact information, including work email and mobile phone numbers, for individuals based on their name, company details, and social profile URLs.

## Enriching data with FullEnrich

1.  While in a Clay table, click `Add enrichment` and search for `FullEnrich`.
2.  Select any of the `FullEnrich` actions detailed below.
3.  In the modal, you will be asked to `Select FullEnrich account`.
    -   If you have your own account, click `+ Add account` and go through authentication. Otherwise, use the Clay provided key.

### `Action` Find work email

Retrieve a person's work email based on their name, company domain, or social profile URL.

**Inputs**

-   **Full name:** Enter or select a column containing the person's full name.
-   **Company name (optional):** Specify the person's company name if known.
-   **Company domain (optional):** Enter the domain of the company (e.g., [`clay.com`](http://clay.com)) for more accurate results.
-   **Social profile URL (optional):** Provide a URL to the person's LinkedIn or other social profiles to increase accuracy.

### `Action` Find mobile phone

Find a person's mobile phone number based on their name, company domain, or social profile URL.

**Inputs**

-   **Full name:** Enter or select a column containing the person's full name.
-   **Company name (optional):** Specify the person's company name if known.
-   **Company domain (optional):** Enter the domain of the company (e.g., [`clay.com`](http://clay.com)) for more accurate results.
-   **Social profile URL (optional):** Provide a URL to the person's LinkedIn or other social profiles to increase accuracy.

### Run settings

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://101))
