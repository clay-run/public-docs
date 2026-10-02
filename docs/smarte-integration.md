---
title: SMARTe integration
description: Enrich company details and technographics (tech stack), and find emails/phone numbers.
last_synced: 2026-09-28T16:45:50.833Z
---

# SMARTe integration

Enrich company details and find emails/phone numbers.

SMARTe is a data enrichment tool that finds accurate contact and company information.

This integration allows you to enrich your data with company details, contact information, mobile numbers, and work emails.

## **Enriching data with SMARTe**

1.  While in a Clay table, click `Add enrichment` and search for `SMARTe`.
2.  Under `Integrations`, select one of the SMARTe enrichment options.
3.  In the modal, you will be asked to `Select SMARTe account`.
    -   If you have your own account, click `+ Add account` and complete authentication. Otherwise, use the Clay provided key.

### `Action` Enrich Company

Use this action to enrich company data using a social URL, personal email, or full name with company information.

**Inputs**

-   **Company name (Optional)**
-   **Company URL (Optional)**
-   **Company social URL (Optional)**

### `Action` Enrich Contact

Use this action to enrich contact data using a social URL, personal email, or full name with company information. _Required: Starter Plan or above._

**Inputs**

-   **Person's social URL (Optional)**
-   **Person's email address (Optional)**
-   **Person's full name (Optional)**
-   **Company name (Optional)**
-   **Company URL (Optional)**

### `Action` Find **Mobile Number**

Use this action to find a person's mobile number using their social URL, personal email, or full name with company information. _Required: Starter Plan or above._

**Inputs**

-   **Person's social URL (Optional)**
-   **Person's email address (Optional)**
-   **Person's full name (Optional)**
-   **Company name (Optional)**
-   **Company URL (Optional)**

### `Action` Find Work Email

Use this action to find a person's work email using their social URL, personal email, or full name with company information.

**Inputs**

-   **Person's social URL (Optional)**
-   **Person's email address (Optional)**
-   **Person's full name (Optional)**
-   **Company name (Optional)**
-   **Company URL (Optional)**

### `Action` Enrich Company Technographics

Use the SMARTe Enrich company technographics action to check whether a company uses specific technologies. You choose the products, categories, or vendors you're looking for, and SMARTe returns only the technologies at that company that match your filters, up to 10 technologies per row. The 10-technology limit is fixed and can't be changed in the action settings.

**Inputs**

You must provide at least one company identifier **and** at least one technology filter.

-   **Company name, Company URL, or Company LinkedIn URL** (at least one required)
-   **Product, Category, or Vendor** filters (at least one required)

### **Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

## SMARTe technographics credit cost

With the Clay-managed SMARTe account, the Enrich company technographics action costs 4 credits for each technology returned in a row. The following examples show the cost per row:

-   1 matching technology: 4 credits
-   5 matching technologies: 20 credits
-   10 matching technologies (the maximum): 40 credits

If SMARTe finds no matching technologies for a row, that row is refunded and costs nothing.

Example: running the technographics action on 100 companies where each company matches 2 technologies costs 100 × 8 = 800 credits.

## Checking for new technologies later with SMARTe technographics

The SMARTe Enrich company technographics action doesn't return a company's full tech stack. It only returns technologies that match the product, category, and vendor filters you selected when the column ran. Because of this, you can't use a formula on an earlier SMARTe technographics result to look for technologies you didn't include in the original filters.

To check the same companies for additional technologies:

1.  Edit the SMARTe technographics column and add the new products, categories, or vendors to the filters.
2.  Re-run the column on the rows you want to check.

Re-running the column charges credits again for every row, based on the number of technologies returned in the new run. If you add more filters and more technologies match, the re-run can cost more than the first run.

## FAQs

### Am I charged when SMARTe doesn't find a result?

Rows where SMARTe finds nothing are refunded, so they don't cost you anything.
