---
title: Crunchbase integration
description: Access company data including financials, growth metrics, funding
  details, and acquisition history.
last_synced: 2026-04-27T18:09:41.382Z
---

# Crunchbase integration

Access company data including financials, growth metrics, funding details, and acquisition history.

Crunchbase is a business intelligence tool that provides detailed company information and insights.

Through this integration, you can access company data directly in Clay, including financials, growth metrics, funding details, and acquisition history.

## **Enriching data with Crunchbase**

1.  While in a Clay table, click `Add enrichment` and search for `Crunchbase`.
2.  Under `Integrations`, select one of the Crunchbase options.
3.  In the modal, you will be asked to `Select Crunchbase account`.
    -   If you haven't already connected your Crunchbase account, click `+ Add account` and go through authentication. Otherwise, use the Clay provided key.

### `Action` Enrich a company's financials

Access Crunchbase's estimates of a company's financials, including revenue range, valuation, total funding, and number of funding rounds.

**Inputs**

-   **Company domain:** Company website or company's Crunchbase organization URL.

### `Action` Enrich a company's growth insights

View Crunchbase's growth trajectory estimates and the key indicators influencing these estimates.

**Inputs**

-   **Company domain:** Company website or company's Crunchbase organization URL.

### `Action` Enrich a company's funding predictions

Access Crunchbase's predictions about a company's likelihood of receiving funding and the factors influencing these predictions.

**Inputs**

-   **Company domain:** Company website or company's Crunchbase organization URL.

### `Action` Enrich an investment fund's details

View Crunchbase's estimates of an investment fund's fundraising history, including money raised, announcement dates, and creation dates for each vintage.

**Inputs**

-   **Company domain:** Company website or company's Crunchbase organization URL.

### `Action` Enrich a company's latest funding round

Get details about a company's most recent funding round, including date, type, and amount.

**Inputs**

-   **Company domain:** Company website or company's Crunchbase organization URL.

### `Action` Enrich a company's acquisitions

Get a list of acquisitions for a company.

**Inputs**

-   **Company domain:** Company website or company's Crunchbase organization URL.

### `Action` Enrich a company's investors

Get a list of investors for a company.

**Inputs**

-   **Company domain:** Company website or company's Crunchbase organization URL.

### `Action` Enrich a company's basic information

Get essential company details like name, website, headquarters location, and industries.

**Inputs**

-   **Company domain:** Company website or company's Crunchbase organization URL.

### **Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

## FAQs

### Can I use Crunchbase data to find companies that may be seeking capital or funding?

Yes. The **Enrich a company's funding predictions** action surfaces Crunchbase's statistical predictions of a company's likelihood of receiving funding, along with the factors influencing those predictions. Add this enrichment to a company table and sort or filter by the funding likelihood score to prioritize outreach to companies most likely to be in fundraising mode.

To set it up: in your company table, click `Add enrichment`, search for `Crunchbase`, and select **Enrich a company's funding predictions**. A Crunchbase API key is required — click `+ Add account` in the setup modal to authenticate.

To complement this with real-time monitoring, pair it with Clay's **Monitor for news & fundraising** signal (select **Fundraising** as the news topic) — that signal fires whenever a company in your list appears in fundraising-related news articles such as funding round announcements.
