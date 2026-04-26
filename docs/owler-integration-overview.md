---
title: Owler integration overview
source_url: https://university.clay.com/docs/owler-integration-overview
description: Business intelligence platform offering competitive insights, lead
  generation, and real-time alerts.
last_synced: 2026-04-26T01:40:27.363Z
upstream_hash: 3d59464c67a625c7ffa9a043899cbceac2b53af50dace7063cbe2e292cff39cd
---

# Owler integration overview

Business intelligence platform offering competitive insights, lead generation, and real-time alerts.

## Overview

Owler in Clay allows users to quickly find company updates, enrich company data, and identify competitors by simply providing a company's domain.

## Setting up Owler and Clay

You can connect and pay for your Owler actions with two options.

1.  **Clay-managed account**: Utilize your Clay Credits to pay for Owler actions.
2.  **(Only available to paid Clay users) Owler account via API key**: Use your Owler account by entering your API key into Clay.

## **Available Actions with the Owler Integration**

### `Action` Find Company Updates

Use this action to retrieve recent company updates, including news, press releases, funding, acquisitions, personnel changes, blogs, or videos, using Owler’s Public Timeline API.

**Setup Inputs**

-   **Company Domain**: Enter or select a column containing the company domain (e.g., [google.com](http://google.com)).
-   **Update Categories** (Optional): Specify categories of updates to filter the results. Multiple categories can be selected.
-   **Limit** (Optional): Define the number of updates to retrieve (maximum: 20). Defaults to 20, sorted by most recent first.

### `Action` Enrich Company

Use this action to convert a given location into standardized geographical data using Owler’s Geocoding API.

**Setup Inputs**

-   **Location**: Enter or select a column containing the location to be normalized.

### `Action` Find Company Competitors

Use this action to retrieve information about a company’s competitors using Owler’s competitive intelligence data.

**Setup Inputs**

-   **Company Domain**: Enter or select a column containing the company domain (e.g., [google.com](http://google.com)).
