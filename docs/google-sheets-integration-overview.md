---
title: Google Sheets integration
source_url: https://university.clay.com/docs/google-sheets-integration-overview
description: Cloud-based spreadsheet for real-time collaboration.
last_synced: 2026-04-26T01:40:04.431Z
---

# Google Sheets integration

Cloud-based spreadsheet for real-time collaboration.

Google Sheets in Clay enables seamless integration between your Clay tables and Google Sheets, allowing you to easily sync and manage data across both platforms.

## Using Google Sheets as a source

You can use a Google Sheet as the source for a Clay table, importing your spreadsheet rows directly into Clay.

When you import from Google Sheets, all columns from your spreadsheet are stored together inside a single **Google Sheets Row** column in Clay. Your Clay table will show only three columns by default — **Google Sheets Row**, **Created At**, and **Updated At** — regardless of how many columns your spreadsheet contains.

**To see all your spreadsheet columns:**

1.  Click any row in your table to open the row details panel.
2.  Switch to the **Values** tab.
3.  Expand the **Google Sheets Row** entry to see all the individual fields from your spreadsheet.

**To reference a specific spreadsheet column in Clay** (e.g., in an enrichment, formula, or AI prompt), use the `/column name` syntax — for example, `/First Name` or `/Email`. You don't need to add every spreadsheet column to your table as a separate Clay column to use the data.

## **Enriching data with Google Sheets**

1.  While in a Clay table, click `Actions` and search for `Google Sheets`.
2.  Under `Enrichments`, select one of the Google Sheets options.
3.  In the modal, you will be asked to `Select Google Sheets account`.
    -   If you haven't already connected your Google Sheets, click `+ Add account` and go through authentication.

### `Action` Add row

Add a row to a Google Sheet via its URL.

**Inputs**

-   **Google Spreadsheet URL**

### `Action` Lookup row

Lookup a row in a Google Sheet using a column and a value.

**Inputs**

-   **Google Spreadsheet URL**

### `Action` Lookup, add, or update row

Lookup a row in a Google Sheet using a column and a value. Optionally, you can add a row if nothing is found, or update a row if something is found.

**Inputs**

-   **Google Spreadsheet URL**

### **Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))
