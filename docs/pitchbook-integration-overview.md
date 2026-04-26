---
title: PitchBook integration
source_url: https://university.clay.com/docs/pitchbook-integration-overview
description: Enrich private and public companies with comprehensive business data.
last_synced: 2026-04-26T01:40:28.992Z
upstream_hash: d9f55ddcea7c9efdc42d84a2a6c59fdcd2aad9ed724642f787e923da0824a05a
---

# PitchBook integration

Enrich private and public companies with comprehensive business data.

PitchBook is a financial data company that provides comprehensive data on the private and public equity companies.

This integration helps you find insights into company ownership status, business status, and financing information.

## Enriching data with PitchBook

To set up the PitchBook integration, start by connecting your Pitchbook account to Clay via an API key:

1.  While in a Clay table, click `Add enrichment` and search for `PitchBook`.
2.  Under `Integrations`, select one of the PitchBook options.
3.  Select `+ Add Account` to add your PitchBook API key.

### `Action` Enrich company (via PitchBook)

Enrich your company with PitchBook by providing the domain.

**Inputs:**

-   **Company domain:** The domain of the company you want to search for.
-   **Include Latest Fundraising Data (Optional):** Include latest fundraising data in the response. _This will cost additional credits per row._
-   **Include VC Data (Optional):** Include the list of VCs that invested in the company in the response. _This will cost additional credits per row._
