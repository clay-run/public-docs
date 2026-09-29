---
title: Pursuit integration
description: Enrich public sector accounts and contacts, find buying signals, and search U.S. government and public sector organizations.
last_synced: 2026-09-29T00:00:00.000Z
---

# Pursuit integration

Enrich public sector accounts and contacts, find buying signals, and search U.S. government and public sector organizations.

Pursuit is a public sector intelligence platform that provides data on U.S. government agencies, school districts, municipalities, counties, and other public sector organizations. Use Pursuit in Clay to enrich public sector accounts and contacts, surface buying signals, and build targeted lists of public sector accounts to prospect into. You can use the Clay-managed Pursuit account or connect your own.

## Using Pursuit in Clay

1. While in a Clay table, click `Add enrichment` and search for `Pursuit`.
2. Under `Integrations`, select the Pursuit action you want to use.
3. Choose to use your own Pursuit API key or the Clay-managed account.

### `Source` Search public sector accounts

Import a list of U.S. public sector accounts as rows in a Clay table, filtered by account type, state, or name.

This source is available for workspaces with the Pursuit accounts source enabled — contact Clay support to request access.

To use this source, click **Add source** and select **Search public sector accounts**. Filter by account type (e.g. school district, municipality, county), U.S. state or territory, or name keywords. Each imported row includes a **Pursuit account ID** for use in enrichment actions.

### `Source` Find public sector signals

Import public sector buying signal events as rows in a Clay table for a defined set of accounts.

This source is available for workspaces with the Pursuit signals source enabled — contact Clay support to request access.

To use this source, click **Add source** and select **Find public sector signals**. Provide a profile description of the type of account you're targeting and the signal criteria you care about. The source returns signal events matching your criteria.

### `Action` Enrich a public sector account

Return detailed information about a U.S. public sector organization.

**Inputs**

Provide a Pursuit account ID, or provide both a company name and U.S. state or territory:

- **Company name (Required if no Pursuit ID):** The name of the public sector organization.
- **Company state or territory (Required if no Pursuit ID):** The full name or two-letter abbreviation of the U.S. state or territory, e.g. `California` or `CA`.
- **Company domain (Optional):** Improves match precision when provided.
- **Pursuit account ID (Alternative):** The Pursuit internal ID for the account. Obtained from the Search public sector accounts source.

**Output**

Returns account details including organization name, type, state, contact information, and other public sector firmographic data.

### `Action` Enrich a public sector contact

Return detailed information about a contact at a U.S. public sector organization.

**Inputs**

Provide a Pursuit account ID, or provide both a company name and U.S. state or territory, along with contact-level identifiers (name, title, or email).

**Output**

Returns contact details including name, title, email, phone, and their associated public sector organization.

### `Action` Find public sector signals for an account

Return buying signal events for a specific public sector account.

**Inputs**

- **Profile description (Required):** A description of the type of public sector account you're targeting.
- **Signal criteria (Required):** The signal type or criteria you want to monitor.
- **Pursuit account ID** or **account name + state** to identify the account.

**Output**

Returns a list of signal events with signal type, date, description, and associated account information.
