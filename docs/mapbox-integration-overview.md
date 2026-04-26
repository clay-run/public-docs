---
title: Mapbox integration
source_url: https://university.clay.com/docs/mapbox-integration-overview
description: AI-powered maps, navigation, and location data.
last_synced: 2026-04-26T01:40:19.819Z
upstream_hash: f3f68ef6315d8ce2e9685106efb634f456c706a140797074ae28ab9179066490
---

# Mapbox integration

AI-powered maps, navigation, and location data.

Mapbox Integration offers advanced location standardization and enrichment, ensuring accurate geographical data for enhanced workflow consistency and precision in targeting.

With this integration, you can standardize addresses, assess geographic proximity, and leverage location data for personalized outreach strategies.

## **Enriching data with Mapbox**

1.  While in a Clay table, click `Add enrichment` and search for `Mapbox`.
2.  Under `Integrations`, select any of the actions detailed below.
3.  In the modal, you will be asked to `Select Mapbox account`.
    -   If you have your own account, click `+ Add account` and go through authentication. Otherwise, use the Clay provided key.

### `Action` Normalize Location

Use this action to standardize and enrich location data to ensure consistency and accuracy for downstream workflows.

**Inputs**

-   **Location:** Full address or location description (e.g., `119 N 11th St, Brooklyn, NY 11249` or `Tokyo, Japan`)

**Output**

-   **Place Name:** Full formatted address
-   **Street Address:** Street number and name
-   **Neighborhood:** Local area name
-   **Postcode:** Postal/ZIP code
-   **Locality:** City/town name
-   **Place:** Major city/municipality
-   **District:** County/district
-   **Region:** State/province
-   **Country:** Country name
-   **Coordinates:** Latitude/longitude coordinates
-   **Location Type:** Classification of the location (e.g., `address`, `place`, `country`)
-   **Accuracy:** Precision level of the geocoding result

### `Action` Find Distance Between Two Locations

Use this action to calculate the distance and travel duration between two locations to assess proximity for targeted outreach.

**Inputs**

-   **Starting Location:** The address or location to start from (e.g., `65 West River Road, Tucson, AZ 85704`)
-   **Ending Location:** The destination address or location (e.g., `119 N. 11th St, Brooklyn, NY 11249`)
-   **Mode of Transport (Optional):** Choose between:
    -   Driving (default)
    -   Walking
    -   Cycling

**Output**

-   **Distance:** Measurements in miles and meters
-   **Estimated travel duration:** Formatted as hours, minutes, and seconds
-   **Location details:** For both starting and ending points:
    -   Full addresses
    -   Geocoordinates
-   **Mode of transport:** Used for the calculation

_Note: Results are displayed with these icon indicators._

-   🚗 For driving routes
-   🚶 For walking routes
-   🚲 For cycling routes

Example: `🚗 2397.86 mi (37h 59m 54s)`

### **Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

## Troubleshooting

### "One of your locations could not be converted into a geocode.”

To solve this error code, try adding the country to your locations.
