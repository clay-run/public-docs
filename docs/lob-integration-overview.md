---
title: Lob integration overview
description: Automated direct mail marketing platform
last_synced: 2026-04-26T01:40:16.885Z
---

# Lob integration overview

Automated direct mail marketing platform

## Lob Overview

The Lob integration allows you to validate and format postal addresses within Clay workflows using Lob's Address Verification API. Use this integration to verify that U.S. and international addresses are real, correctly formatted, and deliverable.

## Setting up Lob and Clay integration

To set up the Lob integration, connect your Lob account by adding your API key. You can access this in the **Settings > Connections** or via any integration panel.

For more help, visit Lob's [documentation](https://help.lob.com/account-management/api-keys) on where to find your API key.

## **Available Actions with the Lob Integration**

### `Action` Validate International Address

Use this action to validate and format a non-U.S. address within Clay workflows using Lob's International Address Verification API.

**Setup Inputs**

-   **Country**: Select the 2-letter ISO 3166 country code for the address. Use the Validate U.S. Address action instead for U.S. addresses.
-   **Primary Line**: Enter or select a column containing the primary delivery line (usually the street address).
-   **Secondary Line** *(optional)*: Enter a secondary delivery line if the address requires one (e.g., apartment or suite number).
-   **City** *(optional)*: The name of the city.
-   **State** *(optional)*: The name of the state or province.
-   **Postal Code** *(optional)*: The postal code of the address.

### `Action` Validate U.S. Address

Use this action to validate and format a U.S. address within Clay workflows using Lob's Address Verification API.

**Setup Inputs**

-   **Full Address**: Enter or select a column containing the full U.S. address to validate, e.g., "123 Main St, San Francisco, CA 94105."
