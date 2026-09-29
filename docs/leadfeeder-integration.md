---
title: Leadfeeder integration
description: Search and enrich European companies and contacts with Leadfeeder firmographic, hierarchy, and contact data.
last_synced: 2026-09-29T00:00:00.000Z
---

# Leadfeeder integration

Search and enrich European companies and contacts with Leadfeeder firmographic, hierarchy, and contact data.

Leadfeeder is a B2B data provider with proprietary EMEA company and contact data. With this integration you can enrich company firmographics, find people at companies, and enrich contact records. A source action for searching and importing company lists is currently in beta.

## Using Leadfeeder in Clay

1.  While in a Clay table, click `Add enrichment` and search for `Leadfeeder`.
2.  Under `Integrations`, select one of the Leadfeeder actions.
3.  In the modal, you will be asked to `Select Leadfeeder account`.
    -   You can use the Clay-managed Leadfeeder account, or bring your own key.
    -   To bring your own, click `+ Add account` and enter your Leadfeeder API key.

### `Source` Find companies with Leadfeeder

Search Leadfeeder for companies and add them to a table. Returns Leadfeeder company IDs and basic company summaries. Use the Leadfeeder company IDs returned here as inputs for the **Enrich company** and **Find people at company** actions.

**Currently in beta — contact support to enable.**

### `Action` Enrich company

Enrich a company using its Leadfeeder company ID, or match it by domain and optional company name. Returns all registered entities with the highest match score.

**Inputs**

Provide at least one of:

-   **Leadfeeder company ID** — returned by the Find companies with Leadfeeder source
-   **Company domain** — e.g. `company.com`
-   **Company name** — combined with **Country** to narrow the match

### `Action` Find people at company

Find and enrich people at a specific company using Leadfeeder's proprietary EMEA company and contact data.

**Inputs**

-   **Leadfeeder company ID (Required):** The Leadfeeder ID of the company where you want to find people. You can find this from the Find companies with Leadfeeder source or the Enrich company action.
-   **Positions (Optional):** Position phrases to filter by, e.g. CEO or Chief Executive Officer.

### `Action` Enrich contact

Enrich a contact using Leadfeeder contact-search filters.

**Inputs**

Contact search filters are used to find the contact record. Provide at least one identifier such as a name, email, or company.
