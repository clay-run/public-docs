---
title: Typeform integration
description: Interactive forms and surveys for gathering customer insights and feedback.
last_synced: 2026-04-26T01:40:50.310Z
---

# Typeform integration

Interactive forms and surveys for gathering customer insights and feedback.

## Typeform Overview

With Clay's Typeform integration, you can import responses from your Typeform surveys directly into a Clay table.

## Setting up Typeform Integration

**Step 1: Import Typeform as a source**

If you are in a new workbook, navigate to the source panel, select all sources, and add Typeform as a source to a Clay table.  

If you are in a table, go to Tools → Import and select Typeform as a source.

**Step 2: Connect Your Typeform Account**

Log in to your Typeform account to link it with Clay. This connection will let you import Typeform responses directly into your Clay table.

**Important:** The Typeform account you connect must be an **owner** of the Typeform workspace that contains the forms you want to import. A workspace member with view-only access is not sufficient — Typeform will reject the connection with a permissions error. If the form was created by a teammate, ask them to either connect their Typeform account to Clay, or grant you owner-level access on that workspace.

**Step 3: Select the form to import**

Choose the Typeform you want to import responses from. Each new response will create an entry in your Clay table.

_Note: To backfill past responses, use a CSV import._

## Troubleshooting

**Typeform import fails / 401 Unauthorized error**

If your Typeform import fails to set up, the most common cause is a permissions mismatch. When you connect a form, Clay registers a webhook on Typeform's API using your connected account. Typeform requires that account to be an **owner** of the workspace that owns the form — workspace members with view access cannot create webhooks.

To resolve:

1. In Typeform, check which workspace owns the form you want to import.
2. Confirm that the Typeform account connected to Clay is an **owner** of that workspace (not just a member).
3. If the form was created by a teammate, either have them connect their Typeform account to Clay instead, or have them grant you owner-level access on that Typeform workspace.
4. Once permissions are updated, go to **Settings → Connections** in Clay, disconnect the Typeform integration, and reconnect using the Typeform account that has owner access.
