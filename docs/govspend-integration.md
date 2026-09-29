---
title: GovSpend integration
description: Search government procurement data in Clay — federal and state contracts, bids, spending records, and agency contacts — to find and qualify public sector buyers.
last_synced: 2026-09-29T00:00:00.000Z
---

# GovSpend integration

Search government procurement data in Clay — federal and state contracts, bids, spending records, and agency contacts — to find and qualify public sector buyers.

GovSpend is a government procurement intelligence platform. With this integration you can enrich government agencies with contact data and bid history and find government contacts such as procurement officers and decision-makers. A source action for importing bids and RFPs into a table is currently in beta.

## Using GovSpend in Clay

1.  While in a Clay table, click `Add enrichment` and search for `GovSpend`.
2.  Under `Integrations`, select one of the GovSpend actions.
3.  In the modal, you will be asked to `Select GovSpend account`.
    -   You can use the Clay-managed GovSpend account, or bring your own key.
    -   To bring your own, click `+ Add account` and enter your GovSpend API key.

### `Source` Find bids and RFPs

Import state and local bids and RFPs, with enough detail to decide which ones are worth pulling documents for.

**Currently in beta — contact support to enable.**

**Inputs** (at least one required)

-   **Keyword:** Words to match against bid title, description, summary, and bid number.
-   **Agency name:** Limit results to one agency by name, e.g. “City of Dallas”.
-   **Agency ID:** GovSpend agency ID — more precise than agency name.
-   **State, City, County**
-   **Agency type:** Airports, Counties, Education, Federal, Fire, Higher Ed, Hospitals, K12 Districts, Law Enforcement, Municipalities, and more.

### `Action` Get bid document details

Get the full description, summary, and attached documents for a single bid.

**Inputs**

-   **Bid ID (Required):** The GovSpend bid ID returned by the Find bids and RFPs source.

### `Action` Enrich agency

Get an agency's basic details, population size, and employee count.

**Inputs**

-   **Agency name or ID (Required)**

### `Action` Enrich agency's aggregated bid activity

Get an agency's bid volume over time, including totals and per-year counts.

**Inputs**

-   **Agency ID (Required)**

### `Action` Enrich employee count by criteria

Count an agency's known contacts, broken down by occupation, job title, and state.

**Inputs**

Agency identifier and optional filter criteria.

### `Action` Enrich person

Get a government contact's role, department, agency, and contact information.

**Inputs**

-   **Person identifier (Required)**

### `Action` Find people

Find government and vendor contacts — procurement officers, decision-makers, and department heads.

**Inputs**

Search filters for name, agency, job title, and location.
