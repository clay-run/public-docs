---
title: Enigma integration
source_url: https://university.clay.com/docs/enigma-integration
description: Enigma is a business intelligence platform that provides accurate
  identity, payment technographic, and financial data on U.S. businesses. With
  this…
last_synced: 2026-04-26T01:39:55.879Z
upstream_hash: 6f20219ee438913db58c2d82e6c96ae821fb9e2c6a396f47468f8f5c8fd2a43b
---

# Enigma integration

Enigma is a business intelligence platform that provides accurate identity, payment technographic, and financial data on U.S. businesses. With this integration, you can enrich company records in Clay with Enigma's identity resolution, operating location data, payment technology detection, and card transaction metrics.

## Enriching data with Enigma

1.  While in a Clay table, click `Add enrichment` and search for `Enigma`.
2.  Under `Integrations`, select one of the Enigma actions.
3.  In the modal, you will be asked to `Select Enigma account`.
    -   If you haven't already connected your Enigma account, click `+ Add account` and enter your API key. You can find your API key in your [Enigma console](https://console.enigma.com/).

**Note:** Enigma's data covers U.S. businesses only. An active Enigma account with API access is required to use this integration.

### `Action` Resolve company identity

Resolve a company's brand name, legal name, and website using partial company identifiers.

**Inputs:**

Required:

-   Company domain: The domain of the company you are trying to resolve. (Required if Company name or Legal company name is not provided.)
-   Company name: The brand name of the company you are trying to resolve, e.g. `Clay`. (Required if Company domain or Legal company name is not provided.)
-   Legal company name: The legal name of the company you are trying to resolve, e.g. `Clay Labs Inc`. (Required if Company domain or Company name is not provided.)

Optional:

-   Street address 1: The first line of the company's street address. Only US addresses are supported.
-   Street address 2: The second line of the company's street address. Only US addresses are supported.
-   City: The city of the company. Only US addresses are supported.
-   State: The state of the company. Only US addresses are supported.
-   ZIP code: The ZIP code of the company. Only US addresses are supported.

**Outputs:**

-   Legal Entity Name: The legal entity name of the company.
-   Company Name: The brand name of the company.
-   Company Website: The website URL of the company.

### `Action` Find person's company affiliations

Find the companies, brands, or websites associated with a specific person.

**Inputs:**

Required:

-   First name: The first name of the person you are looking up company affiliations for.
-   Last name: The last name of the person you are looking up company affiliations for.

Optional:

-   Max company affiliations to return: The maximum number of company affiliations to return. Defaults to `10`, maximum is `100`. Costs 0.4 or 0.2 credits per company affiliation depending on your plan.

**Outputs:**

-   Company name: The brand name of the top affiliated company.
-   Company website: The website of the top affiliated company.
-   Legal entity name: The legal entity name of the top affiliated company.
-   Number of affiliations requested: The total number of affiliations returned.
-   Company affiliations: An array of all returned company affiliations, each containing:
    -   Job title: The person's job title at the affiliated company.
    -   Company name: The brand name of the affiliated company.
    -   Company website: The website of the affiliated company.
    -   Legal entity name: The legal entity name of the affiliated company.

### `Action` Get operating location addresses

Retrieve the physical addresses for all operating locations associated with a brand. A maximum of 100 operating locations can be returned.

**Inputs:**

Required:

-   Company domain: The domain of the company. (Required if Company name is not provided.)
-   Company name: The name of the company. (Required if Company domain is not provided.)

Optional:

-   Max operating locations to return: The maximum number of operating locations to return. Defaults to `10`, maximum is `100`. Costs 0.8 credits per operating location returned.

**Outputs:**

-   Operating Locations: An array of physical address strings for each operating location (e.g., `410 TERRY AVE N SEATTLE WA 98109`).
-   Operating Location Requested Count: The number of operating locations returned.

### `Action` Get operating location count

Count the total number of operating locations a brand operates.

**Inputs:**

Required:

-   Company domain: The domain of the company. (Required if Company name is not provided.)
-   Company name: The name of the company. (Required if Company domain is not provided.)

Optional:

-   Street address 1: The first line of the company's street address. Only US addresses are supported.
-   Street address 2: The second line of the company's street address. Only US addresses are supported.
-   City: The city of the company. Only US addresses are supported.
-   State: The state of the company. Only US addresses are supported.
-   ZIP code: The ZIP code of the company. Only US addresses are supported.

**Outputs:**

-   Operating location count: The total number of operating locations associated with the brand.

### `Action` Get payment technologies

Identify payment technologies used by a brand's operating locations and website.

**Inputs:**

Required:

-   Company domain: The domain of the company. (Required if Company name is not provided.)
-   Company name: The name of the company. (Required if Company domain is not provided.)

Optional:

-   Street address 1: The first line of the company's street address. Only US addresses are supported.
-   Street address 2: The second line of the company's street address. Only US addresses are supported.
-   City: The city of the company. Only US addresses are supported.
-   State: The state of the company. Only US addresses are supported.
-   ZIP code: The ZIP code of the company. Only US addresses are supported.

**Outputs:**

-   Number of Operating Location Payment Technologies: The count of payment technologies detected at the company's operating locations.
-   Number of Website Payment Technologies: The count of payment technologies detected on the company's website.
-   Number of Payment Technologies: The total combined count of payment technologies detected.
-   Operating Location Payment Technologies: An array of payment technology names detected at operating locations (e.g., `Square`).
-   Website Payment Technologies: An array of payment technology names detected on the website (e.g., `Square`).

### `Action` Get 12-month card revenue

Fetch the estimated card transaction revenue for a company over the last 12 months.

**Inputs:**

Required:

-   Company domain: The domain of the company. (Required if Company name is not provided.)
-   Company name: The name of the company. (Required if Company domain is not provided.)

Optional:

-   Street address 1: The first line of the company's street address. Only US addresses are supported.
-   Street address 2: The second line of the company's street address. Only US addresses are supported.
-   City: The city of the company. Only US addresses are supported.
-   State: The state of the company. Only US addresses are supported.
-   ZIP code: The ZIP code of the company. Only US addresses are supported.

**Outputs:**

-   12-Month Card Revenue Projected Quantity: The estimated total card transaction revenue over the last 12 months.

### `Action` Get 12-month average transaction size

Fetch the average card transaction size for a company over the last 12 months.

**Inputs:**

Required:

-   Company domain: The domain of the company. (Required if Company name is not provided.)
-   Company name: The name of the company. (Required if Company domain is not provided.)

Optional:

-   Street address 1: The first line of the company's street address. Only US addresses are supported.
-   Street address 2: The second line of the company's street address. Only US addresses are supported.
-   City: The city of the company. Only US addresses are supported.
-   State: The state of the company. Only US addresses are supported.
-   ZIP code: The ZIP code of the company. Only US addresses are supported.

**Outputs:**

-   12-Month Average Card Transaction Size Projected Quantity: The average value per card transaction over the last 12 months.

### `Action` Get 12-month card growth rate

Retrieve the year-over-year card transaction growth rate for a company over the last 12 months.

**Inputs:**

Required:

-   Company domain: The domain of the company. (Required if Company name is not provided.)
-   Company name: The name of the company. (Required if Company domain is not provided.)

Optional:

-   Street address 1: The first line of the company's street address. Only US addresses are supported.
-   Street address 2: The second line of the company's street address. Only US addresses are supported.
-   City: The city of the company. Only US addresses are supported.
-   State: The state of the company. Only US addresses are supported.
-   ZIP code: The ZIP code of the company. Only US addresses are supported.

**Outputs:**

-   12-Month Card Growth Rate Projected Quantity: The year-over-year card transaction growth rate for the last 12 months.

### `Action` Get 3-month card growth rate

Retrieve the year-over-year card transaction growth rate for a company over the last 3 months.

**Inputs:**

Required:

-   Company domain: The domain of the company. (Required if Company name is not provided.)
-   Company name: The name of the company. (Required if Company domain is not provided.)

Optional:

-   Street address 1: The first line of the company's street address. Only US addresses are supported.
-   Street address 2: The second line of the company's street address. Only US addresses are supported.
-   City: The city of the company. Only US addresses are supported.
-   State: The state of the company. Only US addresses are supported.
-   ZIP code: The ZIP code of the company. Only US addresses are supported.

**Outputs:**

-   3-Month Card Growth Rate Projected Quantity: The year-over-year card transaction growth rate for the last 3 months.

### `Action` Get 12-month average transaction count

Retrieve the total number of card transactions for a company over the last 12 months.

**Inputs:**

Required:

-   Company domain: The domain of the company. (Required if Company name is not provided.)
-   Company name: The name of the company. (Required if Company domain is not provided.)

Optional:

-   Street address 1: The first line of the company's street address. Only US addresses are supported.
-   Street address 2: The second line of the company's street address. Only US addresses are supported.
-   City: The city of the company. Only US addresses are supported.
-   State: The state of the company. Only US addresses are supported.
-   ZIP code: The ZIP code of the company. Only US addresses are supported.

**Outputs:**

-   12-Month Card Transaction Count Projected Quantity: The total number of card transactions over the last 12 months.

### Run settings

-   `Auto-update`: Automatically re-runs the enrichment when a row changes. Recommended when your input data (e.g., company domain or name) may be updated over time and you want Enigma results to stay current.
-   `Only run if`: The enrichment will only run if specified conditions are met. [Learn more about conditional formulas here!](https://www.clay.com/university/guide/conditional-formulas)

## FAQs

### What businesses does Enigma cover?

Enigma's data covers U.S. businesses only. Address fields (street address, city, state, ZIP code) only support U.S. addresses when used as lookup filters.

### Do I need a paid Enigma account to use this integration?

Yes. An active Enigma account with API access is required. You can request access and retrieve your API key from the [Enigma console](https://console.enigma.com/).

### Can I use a company name instead of a domain?

Yes. For most Enigma actions, either a company domain or a company name is sufficient to run the enrichment. Providing both, or adding optional address fields, can help improve match accuracy for companies with common names or multiple locations.

### Why do some actions return a "Projected Quantity" output?

Enigma's card transaction metrics (revenue, growth rate, transaction count, and transaction size) are derived from a large anonymized panel of credit and debit card data and are modeled estimates, not exact figures reported by the business.
