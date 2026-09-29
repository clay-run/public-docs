---
title: Company URL Finder integration
description: Find a company's website domain from their name and country.
last_synced: 2026-09-29T00:00:00.000Z
---

# Company URL Finder integration

Find a company's website domain from their name and country.

The Company URL Finder integration lets you look up a company's website domain using only the company name and country. Use it to fill missing domain fields in your tables before running domain-based enrichments. You can use the Clay-managed Company URL Finder account or connect your own API key.

## Using Company URL Finder in Clay

1. While in a Clay table, click `Add enrichment` and search for `Company URL Finder`.
2. Under `Integrations`, select **Find domain from company name**.
3. Choose to use your own Company URL Finder API key or the Clay-managed account.

### `Action` Find domain from company name

Find a company's website domain from their name.

**Inputs**

- **Company name (Required):** The name of the company to find the domain for.
- **Country (Required):** The country to search in. Results are limited to companies in this country. Defaults to **United States (US)**.

**Output**

- **Domain:** The company's website domain (e.g. `clay.com`).

You are refunded if Company URL Finder finds no result.
