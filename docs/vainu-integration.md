---
title: Vainu integration
description: Enrich Nordic companies with Vainu — registry firmographics plus filed financial statements from the national business registries of Finland, Sweden, Norway, and Denmark.
last_synced: 2026-09-29T00:00:00.000Z
---

# Vainu integration

Enrich Nordic companies with Vainu — registry firmographics plus filed financial statements from the national business registries of Finland, Sweden, Norway, and Denmark.

Vainu provides data sourced directly from the national business registries of Finland (FI), Sweden (SE), Norway (NO), and Denmark (DK). With this integration you can enrich Nordic companies with registry firmographics and financial statement data including revenue, earnings, assets, equity, liabilities, salary costs, and employee counts.

## Using Vainu in Clay

1.  While in a Clay table, click `Add enrichment` and search for `Vainu`.
2.  Under `Integrations`, select one of the Vainu actions.
3.  In the modal, you will be asked to `Select Vainu account`.
    -   You can use the Clay-managed Vainu account, or bring your own key.
    -   To bring your own, click `+ Add account` and enter your Vainu API credentials.

### Common inputs

All Vainu actions require:

-   **Country (Required):** The national business registry to look the company up in — Finland (FI), Sweden (SE), Norway (NO), or Denmark (DK).
-   One of the following company identifiers:
    -   **Company domain** — e.g. `vainu.com`
    -   **Company name** — as registered in the national registry
    -   **Business ID** — official registry ID, country-prefixed (e.g. `FI25578642`) or in the local format (e.g. `2557864-2`)

### `Action` Enrich industry, location and founding date

Returns registry firmographics for a Nordic company: name, legal form, industry and industry codes, registered and visiting addresses, founding date, official status, and company-level contact details.

### `Action` Enrich employee count

Returns the filed employee count for a Nordic company.

### `Action` Enrich company revenue

Returns revenue from a company's filed income statement.

### `Action` Enrich company earnings

Returns earnings from a company's filed income statement.

### `Action` Enrich company equity & liabilities

Returns equity and liabilities from a company's filed balance sheet, broken into equity and liabilities.

### `Action` Enrich company salary costs

Returns salary costs from a company's filed income statement.

### `Action` Enrich company assets

Returns balance sheet assets from a company's filed accounts: total assets, current assets, cash and cash equivalents, and inventory.
