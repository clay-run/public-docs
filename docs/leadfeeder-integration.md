---
title: Leadfeeder integration
description: Enrich B2B company and contact data and find people at companies using Leadfeeder's visitor intelligence platform.
last_synced: 2026-09-29T00:00:00.000Z
---

# Leadfeeder integration

Enrich B2B company and contact data and find people at companies using Leadfeeder's visitor intelligence platform.

Leadfeeder tracks which companies visit your website and provides detailed firmographic and contact data for those companies. In Clay, you can use Leadfeeder to enrich companies, find contacts at companies, and import Leadfeeder company lists as table sources. You can use the Clay-managed Leadfeeder account or connect your own.

## Using Leadfeeder in Clay

1. While in a Clay table, click `Add enrichment` and search for `Leadfeeder`.
2. Under `Integrations`, select the Leadfeeder action you want to use.
3. Choose to use your own Leadfeeder API key or the Clay-managed account.

### `Source` Find companies with Leadfeeder

Import a list of companies from Leadfeeder as rows in a Clay table. Use search filters to narrow the results.

This source is available for workspaces with the Leadfeeder company source enabled — contact Clay support to request access.

To use this source, click **Add source** and select **Find companies with Leadfeeder**. You can filter by company domain, name, VAT ID, country, and other company attributes. Each imported row includes a **Leadfeeder company ID** that you can pass to the Enrich company and Find people at company actions.

### `Action` Enrich company

Enrich a company using a Leadfeeder company ID or company details such as domain, name, VAT ID, or registration ID.

**Inputs**

One of the following is required:

- **Leadfeeder company ID:** The Leadfeeder internal ID for the company. Obtain this from the Find companies with Leadfeeder source.
- **Company details:** Provide at least one of company domain, company name, VAT ID, or registration ID to look up the company by identity.

Additional optional inputs include country and other company attributes to improve match precision.

**Output**

Returns a results array where each match includes:

- **Leadfeeder ID**, **Match score**, **Type**, and an **Attributes** object with address, phone numbers, company name, domain, employee count, industry, revenue, and other firmographic fields.

### `Action` Enrich contact

Find a contact using Leadfeeder contact-search filters.

**Inputs**

Provide at least one contact identifier:

- **Contact name**, **Email addresses**, **Phone numbers**

Optional filters:
- **Company filter: Leadfeeder company ID** — limit results to a specific Leadfeeder company.
- Additional country and demographic filters.

**Output**

Returns a list of matching contacts with name, email, phone, company association, and other contact attributes.

### `Action` Find people at company

Find people associated with a Leadfeeder company.

**Inputs**

- **Leadfeeder company ID (Required):** The Leadfeeder ID of the company. Obtain this from the Find companies with Leadfeeder source or the Enrich company action.
- **Positions (Optional):** Job title phrases to filter by, e.g. `CEO` or `Chief Executive Officer`. Up to 10 values.
- Additional optional contact filters.

**Output**

Returns a list of people at the company with name, email, phone, job title, and related contact information.
