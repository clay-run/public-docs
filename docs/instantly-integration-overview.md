---
title: Instantly integration
description: Automated sales outreach platform.
last_synced: 2026-04-26T01:40:11.630Z
---

# Instantly integration

Automated sales outreach platform.

‍**_\[Update for 2025\] Instantly has released Version 2 of their API keys and will be sunsetting support for Version 1._**

-   **If you are adding your API key, make sure to add version 2.**
-   **For any actively used `Find leads` or `Add Leads to Campaign` columns, you will need to create a new column. (Do not duplicate the original column, create a new one from `Add enrichment`.**

Instantly is an automated sales outreach platform that allows users to efficiently add leads to campaigns.

The Instantly integration in Clay allows users Instantly in Clay allows users to efficiently add leads to campaigns within the app.

## **Setting up the Instantly integration**

**_Note:_** _This integration requires an Instantly API key._

1.  While in a Clay table, click `Add enrichment` and search for `Instantly`.
2.  Under `Integrations`, select one of the Instantly options.
3.  In the modal, you will be asked to `+ Add account`.

## Using the Instantly integration

### `Action` Find leads

Use this action to find new leads.

**Inputs**

-   **Email:** The email of the leads you want to find.
-   **Campaign ID (Optional):** The ID of the campaign you want to search within. If left blank, all leads matching the email will be returned.

**Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

![](https://cdn.prod.website-files.com/687e604972375496b891fe58/691e65a03f3fed1ce9d70f6c_67abd26a6242c505c62de3b8_Random%2520Garbage%2520Frame%25206%2520\(1\).png)

### `Action` Verify Email

Determine if an email address is a valid inbox and whether it's a catch-all domain.

**Inputs**

-   **Person's Email**

**Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

### `Action` Add Lead to Campaign

Add leads to an Instantly campaign.

**Inputs**

-   **Campaign ID**
-   **Skip if Lead is in Workspace (Optional):** Will skip if the lead already exists in any campaigns in the workspace.
-   **Email:** The lead's email.

**Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

### ‍

## Troubleshooting

### Campaign not appearing in the dropdown

If a newly created Instantly campaign doesn't appear in the **Campaign ID** dropdown, do a hard refresh to clear stale browser state:

-   **Mac** — Chrome or Firefox: `Cmd + Shift + R` · Safari: `Cmd + Option + R`
-   **Windows/Linux** — Chrome, Firefox, or Microsoft Edge: `Ctrl + F5`

### "Failed" or "Skipped" results when adding leads

If the **Add Lead to Campaign** action returns a failure or "Skipped" result, the leads may already exist in your Instantly workspace. The action adds leads as new entries via Instantly's create endpoint — it does not update existing records. When a lead already exists in the workspace, the action skips or marks the row as failed rather than overwriting the existing entry.

To resolve this:

1.  Check your Instantly account to confirm whether the leads are already present there.
2.  In your Clay column settings, toggle **Skip if Lead is in Workspace** off.
3.  Re-run the integration.

With **Skip if Lead is in Workspace** disabled, the action will attempt to send the lead to Instantly regardless of whether it already exists in the workspace.
