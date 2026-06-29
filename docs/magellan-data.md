---
title: magellan-data
description: Enrich company records in Clay with corporate ownership, parent company details, and private equity relationships using Magellan Data.
last_synced: 2026-06-29T22:02:41.924Z
---

# Magellan Data

Discover corporate ownership and private equity relationships.

Magellan Data is a B2B data enrichment tool for discovering corporate ownership and private equity relationships. With this integration, you can enrich company records in Clay with parent company details, full corporate family trees, PE ownership information, and PE portfolio companies.

## Enriching data with Magellan Data

1.  While in a Clay table, click `Add enrichment` and search for `Magellan Data`.
2.  Under `Integrations`, select one of the Magellan Data actions.
3.  In the modal, you will be asked to `Select Magellan Data account`.
    -   If you haven't already connected your account, click `+ Add account` and enter your Magellan Data API key. You can find your API key in your Magellan Data account settings.

### `Action` Find Corporate Family

Returns all subsidiaries, divisions, and sister companies within the same corporate family for a given company.

**Inputs**

-   Required:
    -   Company URL or domain: The company URL or domain to look up the corporate family for.
-   Optional:
    -   Limit: The maximum number of corporate family records to return. Minimum is 2. Defaults to 15.

**Outputs**

-   Has parent company: Whether the company has a parent.
-   Is parent company: Whether the company itself is a parent entity.
-   Parent details:
    -   Parent company name: The name of the parent company.
    -   Parent company website: The website of the parent company.
-   Corporate family: An array of related companies within the corporate family, each including:
    -   Child company name: The name of the subsidiary or related company.
    -   Child company website: The website of the subsidiary or related company.
    -   Parent company name: The name of that company's parent.
    -   Parent company website: The website of that company's parent.

### `Action` Find Parent Company

Returns the corporate parent entity for a given company.

**Inputs**

-   Required:
    -   Company URL or domain: The company URL or domain to look up the corporate parent for.

**Outputs**

-   Has parent company: Whether the company has a parent.
-   Parent details:
    -   Parent company name: The name of the parent company.
    -   Parent company website: The website of the parent company.

### `Action` Find PE Owner

Returns the private equity firm that owns a given company, along with the deal type.

**Inputs**

-   Required:
    -   Company URL or domain: The company URL or domain to look up private equity ownership for.

**Outputs**

-   Is PE owned: Whether the company is owned by a private equity firm.
-   Has multiple PE owners: Whether the company has more than one PE owner.
-   Has parent company: Whether the company also has a corporate parent.
-   Parent company name: The name of the corporate parent company, if applicable.
-   Parent company website: The website of the corporate parent, if applicable.
-   PE details:
    -   PE firm name: The name of the private equity firm.
    -   PE firm website: The website of the private equity firm.
    -   Deal type: The type of PE deal (e.g., `control`).

### `Action` Enrich PE Portfolio Companies

Returns all companies currently owned by the same private equity firm as a given company, including add-on acquisitions. Accepts either a portfolio company URL or a PE firm URL as input.

**Inputs**

-   Required:
    -   Company URL or domain: The company URL or domain to look up sibling portfolio companies for. Can be a portfolio company URL or a PE firm URL.
-   Optional:
    -   Limit: The maximum number of portfolio company records to return. Minimum is 2. Defaults to 40.

**Outputs**

-   Is PE owned: Whether the input company is PE-owned.
-   Is PE firm: Whether the input URL belongs to a PE firm.
-   Has multiple PE owners: Whether the company has more than one PE owner.
-   Has parent company: Whether the company also has a corporate parent.
-   Parent company name: The name of the corporate parent, if applicable.
-   Parent company website: The website of the corporate parent, if applicable.
-   PE details: An array of PE firms associated with this company, each including:
    -   PE firm name: The name of the private equity firm.
    -   PE firm website: The website of the private equity firm.

### Run settings

-   `Auto-update`: Recommended when your table is connected to a live CRM or incoming data source so that new company rows are automatically enriched as they arrive.
-   `Only run if`: The enrichment will only run if the specified conditions are met. [**Learn more about conditional formulas here!**](https://docs.clay.com/docs/using-formulas-to-conditionally-run-enrichments)

## Troubleshooting

### Account connects but actions return no data

If your Magellan Data account connects successfully but enrichments return no results, your Magellan account may have insufficient credits. Log in to your Magellan Data account to check your credit balance and purchase additional credits if needed. Note that credits are consumed per record enriched in Clay, regardless of whether data is found.
