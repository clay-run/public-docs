---
title: Airtable integration overview
source_url: https://university.clay.com/docs/airtable-integration-overview
description: Spreadsheet-like database for organizing information and building applications.
last_synced: 2026-04-26T01:39:40.638Z
upstream_hash: c4f3fcef88902fe4aa1b76858d8ca2499bf7bf2de28c10f153a429f64cad74a4
---

# Airtable integration overview

Spreadsheet-like database for organizing information and building applications.

# Airtable Overview

The Airtable integration lets you sync data within your Clay table with your Airtable bases. With this integration you’re able to:

-   Create records
-   Lookup records
-   Update records
-   Upsert records

## Setting up Airtable and Clay

To get set up, you’ll need to add your Airtable account to Clay from either the enrichment panel or the **Settings > Connections** page.

Make sure your linked Airtable account has the right level of access to the bases you want to connect with Clay.

## Available Actions with the Airtable Integration

### `Action` Create records

Create and push a new record to your Airtable directly from Clay.

**Input Fields**:

-   **Base ID** (Required): The ID for the Airtable Base you’d like to create the record in.
-   **Additional Fields**: Any other fields you want to include as part of the record.

### `Action` Lookup records

Check if a specific record exists in your Airtable.

**Input Fields**:

-   **Base ID** (Required): The ID for the Airtable Base you’d like to search within.
-   **Lookup Criteria**: Fields or criteria to define which record to look up.

### `Action` Update records

Modify an existing record in Airtable.

**Input Fields**:

-   **Base ID** (Required): The ID for the Airtable Base you’d like to update.
-   **Record ID**: The unique ID of the record to update.
-   **Fields to Update**: Specify the fields and values to modify.

### `Action` Upsert records

Create or update a record in Airtable based on matching values.

**Input Fields**:

-   **Base ID** (Required): The ID for the Airtable Base where you want to perform the upsert.
-   **Match Criteria**: Fields to match for determining whether to insert or update.
-   **Fields to Include/Update**: Specify fields and values to include in the operation.
