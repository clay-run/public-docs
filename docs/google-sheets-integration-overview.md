---
title: Google Sheets integration
source_url: https://university.clay.com/docs/google-sheets-integration-overview
last_synced: 2026-04-26T01:40:04.431Z
upstream_hash: 0e4fa754fda65b50691a606ea1187287b72e692f52ba0c8b8888f84f6b044f90
---

# Google Sheets integration

Cloud-based spreadsheet for real-time collaboration.

Google Sheets in Clay enables seamless integration between your Clay tables and Google Sheets, allowing you to easily sync and manage data across both platforms.

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
