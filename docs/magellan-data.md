---
title: magellan-data
description: Enrich company records in Clay with corporate ownership, parent company details, and private equity relationships using Magellan Data.
last_synced: 2026-09-24T19:43:06.871Z
---

# Magellan Data integration

Discover corporate ownership and private equity relationships.

Magellan Data is a B2B data enrichment tool for discovering corporate ownership and private equity relationships. With this integration, you can enrich company records in Clay with parent company details, full corporate family trees, PE ownership information, and PE portfolio companies.

## Enriching data with Magellan Data

1.  While in a Clay table, click `Add enrichment` and search for `Magellan Data`.
2.  Under `Integrations`, select one of the Magellan Data actions.
3.  In the modal, you will be asked to `Select Magellan Data account`.
    -   You can run these actions on Clay's shared Magellan Data account, or bring your own key.
    -   To bring your own, click `+ Add account` and enter your Magellan Data API key. You can find your API key in your Magellan Data account settings.

**Note:** `Find corporate family` and `Enrich PE portfolio companies` cost more the more companies they return, so the size threshold on each one doubles as a cost control. Raise it when you want the whole family or portfolio regardless of how large it is, and lower it to skip the very large ones.

### `Action` Find corporate family

Returns all subsidiaries, divisions, and sister companies within the same corporate family for a given company.

**Inputs**

-   Required:
    -   Company URL or domain: The company URL or domain to look up the corporate family for.
-   Optional:
    -   Corporate family size threshold: The action returns the full corporate family or nothing at all, so set this above the family's size — or leave it empty — to capture all of it. The minimum is 2, and it defaults to 15.

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

### `Action` Find parent company

Returns the corporate parent entity for a given company.

**Inputs**

-   Required:
    -   Company URL or domain: The company URL or domain to look up the corporate parent for.

**Outputs**

-   Has parent company: Whether the company has a parent.
-   Parent details:
    -   Parent company name: The name of the parent company.
    -   Parent company website: The website of the parent company.

### `Action` Find PE owner

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

### `Action` Enrich PE portfolio companies

Returns all companies currently owned by the same private equity firm as a given company. Accepts either a portfolio company URL or a PE firm URL as input.

**Inputs**

-   Required:
    -   Company URL or domain: The company URL or domain to look up sibling portfolio companies for. Can be a portfolio company URL or a PE firm URL.
-   Optional:
    -   Portfolio size threshold: The action returns the full portfolio or nothing at all, so set this above the portfolio's size — or leave it empty — to capture all of it. The minimum is 2, and it defaults to 40.

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
-   `Only run if`: The enrichment will only run if the specified conditions are met. [**Learn more about conditional runs here!**](https://university.clay.com/docs/conditional-runs)

## Troubleshooting

### The action finished but returned no ownership data

Magellan Data covers ownership relationships rather than every company, so a company with no parent, no PE owner, and no corporate family simply has no record to return. When that happens the action completes successfully and the cell shows a message like `No Parent Company Found` or `No Portfolio Companies Found` rather than an error.

These runs are refunded, so a company that isn't in Magellan Data's ownership data doesn't cost you credits.

### The action reports that API credits have run out

Magellan Data draws on its own credit balance, separate from your Clay credits, and the message tells you which balance is short.

-   `You are out of credits for this API`: your workspace is running on its own Magellan Data key. Log in to your Magellan Data account to check your balance and top it up.
-   `Clay is out of credits for this API`: you're running on Clay's shared Magellan Data account. Reach out to Clay support and we'll get it topped up.
