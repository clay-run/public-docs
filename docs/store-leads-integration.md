---
title: Store Leads integration
description: Ecommerce data platform for lead generation and market research
  using powerful search filters and API access.
last_synced: 2026-04-26T01:40:43.466Z
---

# Store Leads integration

Ecommerce data platform for lead generation and market research using powerful search filters and API access.

Store Leads is a platform that provides e-commerce data for lead generation. Through Clay's integration, you can enrich company profiles with additional data powered by AI.

## **Finding companies with Store Leads**

Use the **Find companies with Store Leads** source to search the Store Leads database and pull matching e-commerce companies into a Clay table.

1.  In a workbook, click `+ Add` at the bottom and search for `Store Leads`.
2.  Select **Find companies with Store Leads**.
3.  Select your Store Leads account (or use the Clay-provided key).

### `Source` Find companies with Store Leads

Configure filters to narrow your search:

-   **Query** — Free-text search (e.g., "Handmade Soap New York City").
-   **Ecommerce Platform** — Filter to companies on specific platforms. Supports multiple selections.
-   **Technologies** — Filter by installed technologies (comma-separated, e.g., "Facebook Pixel, Google Analytics").
-   **Category** — Filter by product category. Supports multiple selections.
-   **Features** — Filter by store features. Supports multiple selections.
-   **Country** — Filter by company country. Supports multiple selections.
-   **Number of results** — Defaults to 100. Maximum 5,000.
-   **Filters** — Additional property-level filters (e.g., Domain State, Estimated Monthly Revenue).

### Setting an Operation when selecting multiple values

The **Country**, **Category**, **Ecommerce Platform**, and **Features** filters each support multiple selections. When you select more than one value in any of these fields, you **must also set the corresponding Operation field** — otherwise the source returns no results.

The Operation field controls how multiple values are combined:

-   **Any** — Match companies that satisfy at least one of the selected values. Use this for most searches (e.g., companies in the UK *or* the US).
-   **All** — Match companies that satisfy every selected value simultaneously.
-   **None** — Exclude companies that match any of the selected values.

**Example:** To find companies based in either the United Kingdom or the United States, set **Country** to both countries and set **Country Operation** to **Any**.

## **Enriching data with Store Leads**

1.  While in a Clay table, click `Add enrichment` and search for `Store Leads`.
2.  Under `Integrations`, select one of the Store Leads options.
3.  In the modal, you will be asked to `Select Store Leads account`.
    -   If you have your own account, click `+ Add account` and go through authentication. Otherwise, use the Clay provided key.

### `Action` Enrich Company

Use this action to find and enrich company data by using a domain name to obtain detailed data on e-commerce companies, including employee counts, revenue estimates, and social media profiles.

**Inputs**

-   **Company Domain**: Enter or select a column containing the company domain (e.g., [example.com](http://example.com)).

### **Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))
