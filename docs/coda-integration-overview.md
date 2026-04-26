---
title: Coda integration overview
source_url: https://university.clay.com/docs/coda-integration-overview
description: All-in-one workspace for team collaboration.
last_synced: 2026-04-26T01:39:46.493Z
upstream_hash: 87e7b2e8c3a1b643cc9c60cdcd4d8b78edf6ddc3bc3343108d6126d4668abbb1
---

# Coda integration overview

All-in-one workspace for team collaboration.

## Coda Overview

The Coda integration lets you sync data within your Clay table with your Coda bases. With this integration you’re able to:

-   Lookup Row
-   Create or Upsert Row

## Setting up Coda and Clay

To get set up, you’ll need to add your Coda account to Clay from either the enrichment panel or the **Settings > Connections** page.

You’ll add your account by entering your API token which can be obtained from [_My account_](https://coda.io/account) in Coda.

Make sure your linked Coda account has the right level of access to the tables you want to connect with Clay.

## Available Actions with the Coda Integration

### `Action` Lookup Row

Create and push a new record to your Coda directly from Clay.

**Input Fields**:

-   **Doc ID** (Required): The ID for the Coda Doc containing the table.
-   **Table ID** (Required): The ID for the Coda Table to search.
-   **Lookup Criteria**: Specify fields or conditions to identify the row to look up.

### `Action` Create or Upsert Row

Create or upsert a new row in a Coda Table directly from Clay.

**Input Fields**:

-   **Doc ID** (Required): The ID for the Coda Doc containing the table.
-   **Table ID** (Required): The ID for the Coda Table to use.
-   **Additional Fields**: Specify any other fields and values to include or update.
