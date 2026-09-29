---
title: Actovia integration
description: Enrich commercial real estate data with Actovia — property details and sale values, owner portfolios and holdings values, and property contacts with emails and phone numbers.
last_synced: 2026-09-29T00:00:00.000Z
---

# Actovia integration

Enrich commercial real estate data with Actovia — property details and sale values, owner portfolios and holdings values, and property contacts with emails and phone numbers.

Actovia is a commercial real estate data platform. With this integration you can enrich commercial properties with physical details, sale history, and owner portfolio information, find property contacts, and retrieve emails and phone numbers for those contacts.

## Using Actovia in Clay

1.  While in a Clay table, click `Add enrichment` and search for `Actovia`.
2.  Under `Integrations`, select one of the Actovia actions.
3.  In the modal, you will be asked to `Select Actovia account`.
    -   You can use the Clay-managed Actovia account, or bring your own key.
    -   To bring your own, click `+ Add account` and enter your Actovia API key.

### NYC vs. nationwide data

Most property actions include an **Only search New York** toggle:

-   **Enabled (default):** Queries the New York City dataset using BBL (Borough-Block-Lot) records.
-   **Disabled:** Queries the nationwide dataset using APN/parcel-ID records.

Property contact IDs and property IDs are region-specific — if you look up a property with NYC mode on, use NYC mode for any follow-up actions on the same property's contacts or IDs.

### Property lookup inputs

Property actions that look up a specific property accept:

-   **Street address** — e.g. `350 5th Avenue`. Matching is fuzzy; always check the returned matched address.
-   **Borough Block Lot or Parcel ID** — BBL for NYC (e.g. `M-835-41`) or APN/parcel ID for nationwide. Takes precedence when both are provided.

### `Action` Enrich property details

Returns square footage, number of units, number of stories, building class, property type, full address, year built, and modification years for a commercial property.

**Inputs:** Street address or BBL/parcel ID + NYC toggle.

### `Action` Enrich property value

Returns the most recent recorded sale amount and sale date for a commercial property.

**Inputs:** Street address or BBL/parcel ID + NYC toggle.

### `Action` Enrich property value (historical)

Returns the property's assessed market value for the current year and each of the previous 2 years.

**Inputs:** Street address or BBL/parcel ID + NYC toggle.

### `Action` Enrich owner portfolio summary

Returns the number of properties, number of units, total square footage, and property types across an owner's holdings.

**Inputs**

-   **Owner or LLC name (Required)**

### `Action` Enrich owner holdings value

Returns the total value of an owner's property holdings for the current year.

**Inputs**

-   **Owner or LLC name (Required)**

### `Action` Enrich owner holdings value (historical)

Returns the total value of an owner's property holdings for each of the previous 3 years.

**Inputs**

-   **Owner or LLC name (Required)**

### `Action` Find owner's properties

Returns up to 30 addresses and property types an owner holds. `has_more` in the result indicates additional holdings beyond the first 30. Priced per property returned.

**Inputs**

-   **Owner or LLC name (Required)**

### `Action` Find property contacts

Returns up to 6 named contacts tied to a commercial property, each with a contact ID that can be passed to the Find contact email and Find contact phone actions. Priced per contact returned.

**Inputs:** Street address or BBL/parcel ID + NYC toggle.

### `Action` Find contact email

Returns email addresses for a property contact.

**Inputs**

-   **Contact ID (Required):** The contact ID returned by the Find property contacts action.

### `Action` Find contact phone

Returns phone numbers for a property contact.

**Inputs**

-   **Contact ID (Required):** The contact ID returned by the Find property contacts action.
