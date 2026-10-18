---
title: Actovia integration
description: Use Actovia to find NYC and US commercial properties and enrich them with property details, valuations, owner portfolios, and contact information.
last_synced: 2026-09-28T16:56:51.084Z
---

# Actovia integration

Find commercial properties in New York City and across the US, then enrich them with property details, values, owner portfolios, and owner contacts.

Actovia is a commercial real estate data provider with records for New York City properties and for properties nationwide. With this integration, you can build a table of properties that match your criteria, look up a building's size and sale history, size up everything an owner holds, and find named contacts for a property along with their emails and phone numbers.

## **Creating a table with Actovia**

1.  In a workbook, click `+ Add` at the bottom.
2.  Search for `Actovia` and select `Find NYC properties with Actovia` or `Find US properties with Actovia` from the results.
3.  In the modal, you will be asked to `Select Actovia account`.
    -   If you have your own Actovia account, click `+ Add account` and enter your Actovia API key. Otherwise, use the Clay provided key.

**Note:** Both property sources need at least one filter set before they will run. Picking several values inside one filter widens the search, while filters of different kinds narrow it — three boroughs and two property types returns properties in any of those boroughs that are one of those two types.

Both sources filter on `Property types`, and the options depend on which data set you are searching:

| New York City | United States |
| --- | --- |
| IndustrialCo-opVacantCondominiumsGaragesMixed-UseOther1 & 2 Family DwellingLofts_OfficeReligious StructuresHotelsHealthcareMultifamily | AgricultureHealthcareMultifamilyVacant LandCommercial (General)EntertainmentIndustrialUtilitiesOfficeMixed UseParkingRetailSpecial PurposeTransportationHospitalityGovernment/ExemptMiscellaneous |

### `Source` Find NYC properties with Actovia

Import New York City commercial properties that match your filters.

**Inputs**

Every filter is optional, and they sit in four sections in the modal.

-   **`Location`**
    -   **Boroughs:** The boroughs to search — `Manhattan`, `Brooklyn`, `Queens`, `Bronx`, or `Staten Island`. Leave it empty to include every borough.
-   **`Property attributes`**
    -   **Property types:** The property types to include, from the New York City list above. Leave it empty to include every type.
    -   **Number of units:** `Min` and `Max` number of units in the building.
    -   **Square footage:** `Min` and `Max` building square footage.
    -   **Number of stories:** `Min` and `Max` number of floors.
    -   **Year built:** Earliest and latest year of construction.
-   **`Sale & mortgage`**
    -   **Sale amount:** `Min` and `Max` dollar amount for the property's most recent recorded sale.
    -   **Mortgage amount:** `Min` and `Max` dollar amount for the mortgage on the property.
    -   **Sale date start** and **Sale date end:** The window the most recent sale falls in, as `MM/DD/YYYY`.
    -   **Mortgage origination date start** and **Mortgage origination date end:** The window the mortgage was originated in, as `MM/DD/YYYY`.
    -   **Mortgage expiration date start** and **Mortgage expiration date end:** The window the mortgage expires in, as `MM/DD/YYYY`.
-   **`Search limits`**
    -   **Limit:** The maximum number of properties to import. Defaults to 50, and the maximum is 50,000.

**Outputs**

The source creates the following columns:

-   **Address:** The property's full address, like `338 5th Avenue, Midtown, NY, 10118`.
-   **Property type:** Actovia's property type for the building.
-   **BBL / parcel ID:** The property's Borough-Block-Lot identifier, like `M-835-41`.
-   **Street number**, **Street name**, **City**, **State**, and **ZIP code:** The address broken into its parts.
-   **Actovia property ID:** Actovia's own ID for the property, which the source also uses to deduplicate rows across runs.

### `Source` Find US properties with Actovia

Import commercial properties from anywhere in the US that match your filters.

**Inputs**

This source uses the same `Property attributes`, `Sale & mortgage`, and `Search limits` filters as `Find NYC properties with Actovia`, with two location filters in place of boroughs. Choose property types from the United States list above.

-   **`Location`**
    -   **States:** The states to search, listed by two-letter abbreviation. Leave it empty to include every state.
    -   **County:** A single county name, like `Baldwin`. This one is only usable when exactly one state is selected.

**Outputs**

The same columns as `Find NYC properties with Actovia`. `BBL / parcel ID` comes back empty outside of New York City.

## **Enriching data with Actovia**

1.  While in a Clay table, click `Add enrichment` and search for `Actovia`.
2.  Under `Integrations`, select one of the Actovia actions.
3.  In the modal, you will be asked to `Select Actovia account`.

**Note:** Every Actovia action has an `Only search New York` toggle. Leave it on to search New York City records, or switch it off to search records for the rest of the US. Property, owner, and contact IDs belong to one data set or the other, so when you chain actions together, keep the toggle on the same setting all the way through.

### `Action` Enrich property details

Returns the size, type, and matched address of a commercial property.

**Inputs**

Required:

-   **Street address:** The property's street address, like `350 5th Avenue`. (Required if `Borough Block Lot or Parcel ID` is not provided.)
-   **Borough Block Lot or Parcel ID:** The property's exact identifier — a Borough-Block-Lot like `M-835-41` in New York City, or the parcel ID (APN) elsewhere. Takes precedence when `Street address` is also filled in. (Required if `Street address` is not provided.)
-   **Only search New York:** Which data set to query, on for New York City and off for the rest of the US.

**Outputs**

-   **Matched address:** The full address Actovia matched, like `338 5th Avenue, Midtown, NY, 10118`.
-   **Property type:** Actovia's property type for the building, like `Lofts_Office`.
-   **Building class:** The building class code on record, like `O4`.
-   **Stories:** The number of floors.
-   **Units:** The number of units in the building.
-   **Square footage:** The building's total square footage.
-   **Year built:** The year the building was built.
-   **Year first modified** and **Year second modified:** The two most recent years the building was altered.
-   **Street number**, **Street name**, **City**, **State**, and **ZIP code:** The matched address broken into its parts.
-   **BBL / parcel ID:** The matched property's exact identifier.
-   **Actovia property ID:** Actovia's own ID for the property.

### `Action` Enrich property value

Returns the most recent recorded sale for a commercial property.

**Inputs**

The same inputs as `Enrich property details`: `Street address` or `Borough Block Lot or Parcel ID`, plus `Only search New York`.

**Outputs**

-   **Most recent sale amount:** The sale price on the most recent recorded deed, in dollars.
-   **Most recent sale date:** The date of that sale.
-   **BBL / parcel ID** and **Actovia property ID:** Identifiers for the matched property.

### `Action` Enrich property value (historical)

Returns a property's assessed market value for the current year and each of the two years before it.

Actovia has these historical values for New York City properties, so run this action with `Only search New York` on. With the toggle off, the run returns a message letting you know nationwide historical values aren't available yet.

**Inputs**

The same inputs as `Enrich property details`: `Street address` or `Borough Block Lot or Parcel ID`, plus `Only search New York`.

**Outputs**

-   **Market value (current year):** The assessed market value on record for this year.
-   **Market value (1 year ago)** and **Market value (2 years ago):** The assessed market values for the two prior years.
-   **BBL / parcel ID** and **Actovia property ID:** Identifiers for the matched property.

### `Action` Enrich owner portfolio summary

Returns the size and mix of everything an owner holds.

**Inputs**

Required:

-   **Owner or LLC name:** The property owner's name, either a person like `Jane Smith` or an entity like `123 Main Street LLC`. Matching is case-insensitive.
-   **Only search New York:** Which data set to query, on for New York City and off for the rest of the US.

**Outputs**

-   **Number of properties:** How many properties the owner holds.
-   **Total units:** The combined unit count across those properties.
-   **Total square footage:** The combined square footage across those properties.
-   **Property types:** The property types represented in the portfolio.
-   **Matched owner name:** The owner name Actovia matched, so you can confirm it's the right one.
-   **Actovia owner ID:** Actovia's own ID for the owner.

### `Action` Enrich owner holdings value

Returns the total value of an owner's holdings for the current year.

**Inputs**

The same inputs as `Enrich owner portfolio summary`: `Owner or LLC name` and `Only search New York`.

**Outputs**

-   **Total holdings value:** The combined value of the owner's properties, in dollars.
-   **Matched owner name** and **Actovia owner ID:** Identifiers for the matched owner.

### `Action` Enrich owner holdings value (historical)

Returns the total value of an owner's holdings for the current year and each of the two years before it.

**Inputs**

The same inputs as `Enrich owner portfolio summary`: `Owner or LLC name` and `Only search New York`.

**Outputs**

-   **Holdings value (current year):** The combined value of the owner's properties this year, in dollars.
-   **Holdings value (1 year ago)** and **Holdings value (2 years ago):** The same figure for the two prior years.
-   **Matched owner name** and **Actovia owner ID:** Identifiers for the matched owner.

### `Action` Find owner's properties

Returns the addresses an owner holds, up to 30 per run.

**Inputs**

The same inputs as `Enrich owner portfolio summary`: `Owner or LLC name` and `Only search New York`.

**Outputs**

-   **Number of properties:** How many properties this run returned.
-   **Has more properties:** Whether the owner holds more properties than the run returned.
-   **Properties:** One entry per property, each with `Address`, `Property type`, `BBL / parcel ID`, `City`, `State`, and `ZIP code`.

### `Action` Find property contacts

Returns up to 6 named contacts tied to a commercial property, each with the contact ID that the email and phone actions need.

**Inputs**

Required:

-   **Street address:** The property's street address. (Required if `Borough Block Lot or Parcel ID` is not provided.)
-   **Borough Block Lot or Parcel ID:** The property's exact identifier. (Required if `Street address` is not provided.)
-   **Only search New York:** Which data set to query, on for New York City and off for the rest of the US.

Optional:

-   **Owner LLC name filter:** Only return contacts tied to this owner entity, as named on the deed. The name of a company that occupies the building filters out every contact, so leave this empty when you want all of them.

**Outputs**

-   **Number of contacts:** How many contacts came back.
-   **Contacts:** One entry per contact, each with `Name` and `Contact ID`.

### `Action` Find contact email

Returns the email addresses on record for a property contact.

**Inputs**

Required:

-   **Contact ID:** The contact ID exactly as `Find property contacts` returned it, like `c_47605` or `cd_100342`.
-   **Only search New York:** Set this to match the `Find property contacts` run the contact ID came from.

**Outputs**

-   **Email address:** The first email address on record.
-   **Additional email addresses:** Any other email addresses on record.
-   **Number of emails:** How many email addresses came back in total.

### `Action` Find contact phone

Returns the phone numbers on record for a property contact.

**Inputs**

The same inputs as `Find contact email`: `Contact ID` and `Only search New York`.

**Outputs**

-   **Phone number:** The first phone number on record.
-   **Additional phone numbers:** Any other phone numbers on record.
-   **Number of phone numbers:** How many phone numbers came back in total.

### Run settings

-   **Auto-update:** Recommended when rows keep arriving, so new properties, owners, and contacts are enriched as they land.
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

## **FAQs**

### Why did a lookup match a different building than I expected?

Actovia matches on the street line only, so anything after the first comma in `Street address` is dropped, and the match doesn't take a city or borough into account. An address that exists in several places — `770 Broadway`, say — can resolve to a building you didn't have in mind.

Two ways to keep it precise:

-   Check `Matched address` or `BBL / parcel ID` before you rely on the rest of the row.
-   Pass the `Borough Block Lot or Parcel ID` whenever you have it, since identifier lookups are exact.

### How are Actovia actions billed?

Most Actovia actions cost a flat number of credits per row. `Find property contacts` and `Find owner's properties` are priced per record returned, so a property with six contacts costs more than one with a single contact, and the two property sources are billed per property imported.

### Am I charged for rows that don't match?

No. Every action refunds its credits when the lookup comes back empty.

### My run finished but the columns are empty. Why?

Two different outcomes look alike at a glance, and the cell preview tells you which one you got:

-   Actovia has no record matching the address, identifier, or owner name you sent.
-   The record matched, but Actovia has nothing on file for what that action asks for — a building with no recorded sale, or an owner with no valuation on record.

### What do Actovia's capacity messages mean?

Actovia limits how much data it returns, both in a single call and over a rolling window:

-   A lookup whose result set is enormous — an owner holding thousands of properties, for instance — comes back with a message that it's too large for one call. Retrying won't change that, so reach for property-level actions on that owner's individual addresses instead.
-   A capacity quota message means the account has pulled a lot of data recently. The quota recovers over time, which can take a day or more, so run those rows again later.

### Why is my contact ID rejected?

`Find contact email` and `Find contact phone` need the contact ID in exactly the form `Find property contacts` returns it — `c_47605` or `cd_100342`, prefix included. A bare number can belong to two different people, so Clay asks for the prefixed ID rather than risk returning the wrong person's details.
