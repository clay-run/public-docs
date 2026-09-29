---
title: Company URL Finder integration
description: Use Company URL Finder in Clay to automatically resolve and retrieve the correct company website based on a company name input.
last_synced: 2026-09-29T00:00:00.000Z
---

# Company URL Finder integration

Use Company URL Finder in Clay to automatically resolve and retrieve the correct company website based on a company name input.

Company URL Finder resolves company names to their official website domains. With this integration you can fill in missing company domains when you have a company name but no URL, scoped to a specific country.

## Using Company URL Finder in Clay

1.  While in a Clay table, click `Add enrichment` and search for `Company URL Finder`.
2.  Under `Integrations`, select `Find domain from company name`.
3.  In the modal, you will be asked to `Select Company URL Finder account`.
    -   You can use the Clay-managed account, or bring your own key.
    -   To bring your own, click `+ Add account` and enter your Company URL Finder API key.

### `Action` Find domain from company name

Find a company's website domain from their name. Results are limited to companies in the selected country.

**Inputs**

-   **Company name (Required):** The name of the company to find the domain for.
-   **Country (Required):** The country to search in. Defaults to **United States (US)**. Results are limited to companies registered in this country.
