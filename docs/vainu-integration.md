---
title: Vainu integration
description: Enrich Nordic company firmographics and financials including revenue, earnings, equity, employee count, and assets from official business registries in Finland, Sweden, Norway, and Denmark.
last_synced: 2026-09-29T00:00:00.000Z
---

# Vainu integration

Enrich Nordic company firmographics and financials including revenue, earnings, equity, employee count, and assets from official business registries in Finland, Sweden, Norway, and Denmark.

Vainu provides enrichment data sourced directly from national business registries for companies registered in the Nordic countries. Data reflects official filings and covers firmographics, revenue, earnings, employee count, assets, equity, liabilities, and salary costs.

## Connecting Vainu in Clay

Vainu requires your own OAuth client credentials. Create a client in the Vainu platform under **Settings → API Access**, then connect it in Clay.

1. While in a Clay table, click `Add enrichment` and search for `Vainu`.
2. Under `Integrations`, select the Vainu action you want to use.
3. Click `+ Add account` and enter your Vainu Client ID and Client Secret to authenticate.

## Company identifier inputs

All Vainu enrichment actions require a **Country** selection and at least one company identifier:

- **Company domain** — the company's website domain, like `vainu.com`.
- **Company name** — the registered company name.
- **Business ID** — the official registry ID, country-prefixed like `FI25578642` or in local format like `2557864-2`.

**Supported countries:** Finland (FI), Sweden (SE), Norway (NO), Denmark (DK).

### `Action` Enrich industry, location and founding date

Return a company's primary industry code, legal form, country, and founding date from the national business registry.

**Inputs:** Company domain, company name, or business ID, plus country (see above).

**Output**

- **Company name**, **Business ID**, **Legal form**, **Country**, **Founded date**, **Primary industry code**, **Primary industry name**

### `Action` Enrich company revenue

Return a company's revenue and currency from the most recent filed fiscal period.

**Inputs:** Company domain, company name, or business ID, plus country (see above).

**Output**

- **Revenue**, **Currency**, **Fiscal period end**, **Company name**, **Business ID**

### `Action` Enrich company earnings

Return a company's operating profit and net profit from the most recent filed fiscal period.

**Inputs:** Company domain, company name, or business ID, plus country (see above).

**Output**

- **Operating profit/loss**, **Net profit/loss**, **Currency**, **Fiscal period end**, **Company name**, **Business ID**

### `Action` Enrich company equity & liabilities

Return total equity and total liabilities from the most recent filed fiscal period.

**Inputs:** Company domain, company name, or business ID, plus country (see above).

**Output**

- **Total equity**, **Total liabilities**, **Currency**, **Fiscal period end**, **Company name**, **Business ID**

### `Action` Enrich company salary costs

Return total salary costs from the most recent filed fiscal period.

**Inputs:** Company domain, company name, or business ID, plus country (see above).

**Output**

- **Salary costs**, **Currency**, **Fiscal period end**, **Company name**, **Business ID**

### `Action` Enrich company assets

Return total assets and key asset categories from the most recent filed fiscal period.

**Inputs:** Company domain, company name, or business ID, plus country (see above).

**Output**

- **Total assets**, **Current assets total**, **Cash and cash equivalents**, **Inventory**, **Fiscal period end**, **Company name**, **Business ID**

### `Action` Enrich employee count

Return a company's filed employee count from the most recent fiscal period.

**Inputs:** Company domain, company name, or business ID, plus country (see above).

**Output**

- **Employee count**, **Fiscal period end**, **Company name**, **Business ID**
