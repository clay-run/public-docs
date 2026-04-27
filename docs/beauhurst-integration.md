---
title: Beauhurst integration
source_url: https://university.clay.com/docs/beauhurst-integration
description: Beauhurst is a private company intelligence platform covering every
  private company in the UK and Germany. Within Clay, you can use Beauhurst to
  enrich…
last_synced: 2026-04-27T18:09:21.673Z
upstream_hash: 46ba431ca3e7c982151ae46ade2ba4002e67ba5cfb51116f2775557013b81a64
---

# Beauhurst integration

Beauhurst is a private company intelligence platform covering every private company in the UK and Germany. Within Clay, you can use Beauhurst to enrich companies with registration details, funding history, and corporate structure data — purpose-built for UK and German markets.

## Enriching data with Beauhurst

1.  While in a Clay table, click `Add enrichment` and search for `Beauhurst`.
2.  Under `Integrations`, select one of the Beauhurst actions.
3.  In the modal, you will be asked to `Select Beauhurst account`.
    -   If you haven't already connected your Beauhurst account, click `+ Add account` and enter your API key. You can find your API key in your Beauhurst account settings.

**Note:** Beauhurst covers private companies in the **UK and Germany only**. Actions will return no data for companies outside these markets. Credits are refunded when no data is returned.

### `Action` Enrich company (UK & Germany)

Enrich a company using its domain to fetch registration details, address, live status, and contact information.

**Inputs**

Required:

-   Company domain: The domain of the company to enrich.

**Outputs**

-   Name: The company's trading name.
-   Registered Name: The company's full legal registered name.
-   Registration Date: The date the company was incorporated.
-   Other Trading Names: Any additional trading names associated with the company.
-   Company Registration Number: The official registration number (Companies House for UK; equivalent for Germany).
-   Employee Count Range: Banded employee count (e.g., `>1000`).
-   Websites: All website URLs associated with the company.
-   Company Status: The live status of the company (e.g., Active).
-   Is SME: Whether the company qualifies as a small or medium-sized enterprise.
-   Country: The country code of the company's registered country.
-   Region: The regional identifier for the company's location.
-   Address: The company's trading address.
-   Company Telephone: The company's primary phone number.
-   Company Emails: Email addresses associated with the company.
-   Registered Address: The company's official registered address.
-   LinkedIn URL: The company's LinkedIn profile URL.

### `Action` Find company funding (UK & Germany)

Get a company's funding overview using its domain to retrieve raise history, grant totals, and latest valuation.

**Inputs**

Required:

-   Company domain: The domain of the company to look up.

**Outputs**

-   N Fundraisings: The total number of fundraising rounds the company has completed.
-   Total Amount Fundraisings: The total capital raised across all fundraising rounds.
-   N Grants: The total number of grants the company has received.
-   Total Amount Grants: The total value of all grants received.
-   Latest Valuation: The company's most recent known valuation.

### `Action` Find company corporate structure (UK & Germany)

Map a company's corporate structure using its domain to identify its ultimate parent, immediate parent, and all subsidiaries.

**Inputs**

Required:

-   Company domain: The domain of the company to map.

**Outputs**

-   Ultimate Parent: The top-level parent entity in the corporate hierarchy.
    -   Name: The ultimate parent company name.
    -   Company Registration Number: The ultimate parent's registration number.
-   Immediate Parent: The direct parent company one level above.
    -   Name: The immediate parent company name.
    -   Company Registration Number: The immediate parent's registration number.
    -   Country: The country where the immediate parent is registered.
-   All Children: An array of all known subsidiaries.
    -   Name: The subsidiary company name.
    -   Company Registration Number: The subsidiary's registration number.
    -   Country: The country where the subsidiary is registered.

### Run settings

-   **Auto-update:** Turn on auto-update to keep company data current as records are added or change over time. Recommended when using Beauhurst as part of an ongoing enrichment workflow.
-   **Only run if:** The enrichment will only run when specified conditions are met. [**Learn more about conditional formulas here.**](https://www.clay.com/university/guide/conditional-formulas)
