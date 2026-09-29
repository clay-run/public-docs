---
title: Pursuit integration
description: Enrich U.S. public sector accounts and contacts with government identifiers, firmographics, corrected contact details, role-confidence signals, and buying signals.
last_synced: 2026-09-29T00:00:00.000Z
---

# Pursuit integration

Enrich U.S. public sector accounts and contacts with government identifiers, firmographics, corrected contact details, role-confidence signals, and buying signals.

Pursuit is a data provider specializing in U.S. public sector accounts — government agencies, school districts, municipalities, and similar entities. With this integration you can enrich account and contact records and surface buying signals matched to your product profile. Source actions that build lists of public sector accounts are currently in beta.

## Using Pursuit in Clay

1.  While in a Clay table, click `Add enrichment` and search for `Pursuit`.
2.  Under `Integrations`, select one of the Pursuit actions.
3.  In the modal, you will be asked to `Select Pursuit account`.
    -   You can use the Clay-managed Pursuit account, or bring your own key.
    -   To bring your own, click `+ Add account` and enter your Pursuit API key.

### `Action` Enrich a public sector account

Return firmographic and identifier data for a U.S. public sector account, including canonical name, website, coordinates, and population estimates.

**Inputs**

-   **Company name (Required):** The name of the public sector organization.
-   **Company state or territory (Required):** The U.S. state or territory where the organization is located, e.g. California or CA.
-   **Company domain (Optional):** Improves match precision.

### `Action` Enrich a public sector contact

Check a U.S. public sector contact against Pursuit data to determine whether the person is still in role, has moved, or has retired. Returns corrected contact details with a confidence score.

**Inputs**

Provide a Pursuit account ID, or both a company name and U.S. state:

-   **Pursuit account ID** — or —
-   **Company name** + **Company state or territory**

### `Action` Find public sector signals for an account

Return the public sector buying signals for one account, ranked against your product profile and signal criteria.

**Inputs**

Provide a Pursuit account ID, or both a company name and U.S. state:

-   **Pursuit account ID** — or —
-   **Company name** + **Company state or territory**

### `Source` Search public sector accounts

Build a list of U.S. public sector accounts by account type, state, name, website, or population. Returns government identifiers, canonical websites, and coordinates for every match.

**Currently in beta — contact support to enable.**

**Inputs** (at least one filter required)

-   **Account types:** School districts, municipalities, counties, etc.
-   **States or territories:** U.S. states or territories to filter by.
-   **Name includes any of:** Terms to match against account names.
-   **Website**
-   **Population range**

### `Source` Find public sector signals

Find public sector accounts showing buying signals that match your product profile, with a summary and a link to the source document.

**Currently in beta — contact support to enable.**
