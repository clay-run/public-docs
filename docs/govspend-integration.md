---
title: GovSpend integration
description: Enrich U.S. government agencies, find government contacts, and search bids and RFPs using GovSpend's public sector spend intelligence platform.
last_synced: 2026-09-29T00:00:00.000Z
---

# GovSpend integration

Enrich U.S. government agencies, find government contacts, and search bids and RFPs using GovSpend's public sector spend intelligence platform.

GovSpend is a public sector spend intelligence platform covering U.S. federal, state, and local government agencies. Use GovSpend in Clay to enrich agency profiles, find procurement contacts, source bid and RFP opportunities, and understand government purchasing activity. You can use the Clay-managed GovSpend account or connect your own.

## Using GovSpend in Clay

1. While in a Clay table, click `Add enrichment` and search for `GovSpend`.
2. Under `Integrations`, select the GovSpend action you want to use.
3. Choose to use your own GovSpend API key or the Clay-managed account.

### `Source` Find bids and RFPs

Import active government bids and RFPs as rows in a Clay table.

This source is available for workspaces with the GovSpend bids source enabled — contact Clay support to request access.

To use this source, click **Add source** and select **Find bids and RFPs**. Filter results by:

- **Keyword** — words to match against the bid title, description, summary, and bid number.
- **Agency name** — limit to one agency by name, e.g. `City of Dallas`.
- **Agency ID** — GovSpend agency ID for precise agency targeting.
- **State, city, or county** — geographic filters.
- **Agency type** — filter by agency category such as `K12 Districts`, `Municipalities`, `Counties`, `Federal`, `Higher Ed`, `Hospitals`, `Law Enforcement`, and others.

At least one filter is required. Each imported row includes a **bid ID** that you can pass to the Get bid document details action.

### `Action` Enrich agency

Return profile information for a U.S. government agency.

**Inputs**

- **Agency name** or **Agency ID** to identify the agency.

**Output**

Returns agency name, type, level of government, state, contact information, and other agency profile data.

### `Action` Enrich agency's aggregated bid activity

Return bid volume totals and per-year counts for a U.S. government agency.

**Inputs**

- **Agency ID** — the GovSpend agency ID to look up bid activity for.

**Output**

Returns total bid count and a yearly breakdown of bid activity over time.

### `Action` Enrich employee count by criteria

Return the count of known contacts at an agency, broken down by occupation, job title, and state.

**Inputs**

- **Agency ID** and optional filters for occupation, job title, or state.

**Output**

Returns the count of known contacts matching the specified criteria, with breakdown by occupation, job title, and state.

### `Action` Enrich person

Return profile information for a government or vendor contact.

**Inputs**

- **Person identifier** — name, email, or GovSpend person ID.

**Output**

Returns contact name, title, agency affiliation, email, phone, and other contact details.

### `Action` Find people

Find government and vendor contacts — procurement officers, decision-makers, and department heads — matching search criteria.

**Inputs**

- Search by name, title, agency, state, or other contact attributes.

**Output**

Returns a list of matching government contacts with name, title, agency, email, phone, and other profile information.

### `Action` Get bid document details

Return the full description, summary, and attached documents for a single bid.

**Inputs**

- **Bid ID (Required):** The GovSpend bid ID. Obtain this from the Find bids and RFPs source.

**Output**

- **Title**, **Description**, **Summary**, **Documents count**, **Documents** — the full bid details including any attached procurement documents.
