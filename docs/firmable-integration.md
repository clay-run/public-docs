---
title: Firmable integration
description: Find Australian mobile phones and work emails.
last_synced: 2026-04-26T01:40:00.103Z
---

# Firmable integration

Find Australian mobile phones and work emails.

Firmable is an intelligence tool for lead generation and account research.

With this integration, you can automatically enrich your Clay tables with company and contact data from Firmable's extensive Australian database.

## Setting up the Firmable integration

1.  While in a Clay table, click `Add enrichment` and search for Firmable.
2.  Under `Integrations`, select one of the Firmable options.
3.  In the modal, you will be asked to `Select Firmable account`.
    1.  If you have your own account, click `+ Add account` and go through authentication. Otherwise, use the Clay provided key.

## Using the Firmable integration

### `Action` Find mobile phone (Australia)

Retrieves an individual's phone number using the contact's social URL.

**Inputs**

-   **Social URL**

**Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

### `Action` Find work email (Australia)

Retrieves an individual's work email address using the contact's social URL.

**Inputs**

-   **Social URL**

**Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

## Finding personal emails for Australian contacts

The **Find personal email (Australia)** action has been removed from Firmable. Firmable no longer provides personal email data via their API.

To find personal emails for Australian (and global) contacts, use the **Personal Email** waterfall in Clay, which includes providers such as Forager, People Data Labs, Wiza, ContactOut, Limadata, and Mixrank — several of which have solid Australian and global coverage.

## FAQs

### Can I use Firmable to build or import a company list?

No. Firmable is enrichment-only in Clay — it cannot be used as a **source** to import companies or people into a new table. All Firmable actions require an existing contact's LinkedIn URL as input; they return data about Australian contacts you already have, rather than generating a new list.

To build a list of companies in Singapore or another APAC market, use Clay's **Find Companies** source with the **Location** filter set to the target country. Find Companies supports filtering by country, city, state or province, region, and postal code, and works for any region globally.

For additional sourcing options when building Singapore company lists:

-   **Find local businesses using Google Maps** — use the native Google Maps source to discover businesses in a specific city or area.
-   **HTTP API as source** — connect to a public API such as the [Singapore government data API](https://guide.data.gov.sg/developer-guide/dataset-apis/search-and-filter-within-dataset) to import records directly into Clay as a starting point for enrichment.

### Does Firmable cover Singapore or other APAC markets?

No. Firmable focuses solely on Australian people and company data. For contact enrichment in other APAC markets, providers such as SMARTe (strong APAC and mobile coverage) are available in Clay.
