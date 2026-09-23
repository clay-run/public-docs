---
title: Company URL Finder integration
description: Use Company URL Finder in Clay to turn a company name into that company's website domain.
last_synced: 2026-09-23T19:09:02.756Z
---

# Company URL Finder integration

Use Company URL Finder in Clay to turn a company name into that company's website domain.

Company URL Finder is a data provider that matches company names to the websites those companies actually use. With this integration, you can fill in the domain for every company name in a Clay table and keep each lookup scoped to one country, so the company you get back is the one you meant.

## Enriching data with Company URL Finder

1.  While in a Clay table, click `Add enrichment` and search for `Company URL Finder`.
2.  Under `Integrations`, select `Find domain from company name`.
3.  In the modal, you will be asked to `Select Company URL Finder account`.
    -   If you have your own Company URL Finder account, click `+ Add account` and enter your API key. Otherwise, use the Clay provided key.

**Note:** The `Country` field defaults to `United States`, so a list that spans several countries will come back empty for the companies outside it. To set the country row by row instead, click the gear button on `Country` and switch it to the `Text with tokens` input mode, then map a column holding each company's two-letter country code, such as `DE` or `BR`.

### `Action` Find domain from company name

Finds a company's website domain from their name.

**Inputs**

Required:

-   **Company name:** The name of the company you want a domain for.
-   **Country:** The country to search in. Company URL Finder returns only companies based in the country you pick, and the dropdown covers 238 countries and territories.

**Outputs**

-   **Domain:** The company's website domain (e.g., `clay.com`).

### Run settings

-   **Auto-update:** Useful when company names keep arriving, so new rows get a domain as they land instead of waiting for you to re-run the column.
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

## FAQs

### How many credits does this action use?

1 action and 0.6 credits per row when you use the Clay provided key.

### Am I charged for rows where no domain comes back?

No. When Company URL Finder has no match for a name in the country you selected, Clay refunds the credits for that row and the cell shows `No domain found`. Those rows are easy to filter for, so you can re-run them against a different country or send them to another domain-finding action.

### Can I use my own Company URL Finder API key?

Yes. Click `+ Add account` and paste the key, and Clay checks it right away so you know whether it is valid before you run a column. If the key is valid but has no credits left, Clay warns you when you connect it, and rows come back with an out-of-credits message, so top up in Company URL Finder and re-run the column. If you would rather not manage a separate balance, use the Clay provided key instead.

### Will this work on a long list of company names?

Yes. Company URL Finder limits how many lookups it accepts per minute, so Clay paces the column and automatically retries any row that gets held back. A long column takes longer to finish, and you don't need to split it into batches.
