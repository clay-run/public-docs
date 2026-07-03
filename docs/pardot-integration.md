---
title: Pardot integration
description: Manage Salesforce Marketing Cloud Account Engagement (Pardot) prospects,
  lists, and list memberships natively from Clay using your existing Salesforce connection.
last_synced: 2026-07-03T00:00:00.000Z
---

# Pardot integration

Manage Salesforce Marketing Cloud Account Engagement (Pardot) prospects, lists, and list memberships natively from Clay using your existing Salesforce connection.

Pardot (Salesforce Marketing Cloud Account Engagement) is a B2B marketing automation platform built on Salesforce. With this integration, you can look up, create, and update prospects and lists in Pardot — including custom fields — directly from a Clay table.

> **This integration is currently in closed beta.** To request access, contact your account team or reach out to [support@clay.com](mailto:support@clay.com).

## Connecting to Pardot

Pardot uses your existing Salesforce connection — no separate authentication is required. When you add a Pardot enrichment, select your connected Salesforce account and then choose your **Pardot Business Unit** from the dropdown.

If you haven't connected Salesforce to Clay yet, see [Salesforce integration](salesforce-integration-overview.md) for setup instructions.

## Enriching data with Pardot

1.  While in a Clay table, click `Add enrichment` and search for `Pardot`.
2.  Under `Integrations`, select one of the Pardot options.
3.  In the modal, select your Salesforce account.
    -   If you haven't connected your Salesforce account yet, click `+ Add account` and complete authentication.
4.  Select your **Pardot Business Unit** from the dropdown.

## Prospect actions

### `Action` Look up Pardot prospect

Look up a Pardot prospect by email address or prospect ID.

**Inputs**

-   **Pardot Business Unit**
-   **Email address** (optional): Email to search for. Note: multi-select, checkbox, and "Record and display multiple responses" custom fields cannot be returned when looking up by email — use prospect ID if you need those fields.
-   **Prospect ID** (optional): Pardot prospect ID. Takes priority over email if both are provided.

### `Action` Create Pardot prospect

Create a new Pardot prospect.

**Inputs**

-   **Pardot Business Unit**
-   **Email address**: Prospect email address (required).
-   **Prospect fields** (optional): Map standard and custom fields. Standard fields include first name, last name, company, job title, department, phone, address, industry, annual revenue, and more. Custom fields are loaded dynamically from your Pardot account.

### `Action` Update Pardot prospect

Update an existing Pardot prospect by ID.

**Inputs**

-   **Pardot Business Unit**
-   **Prospect ID**: The Pardot prospect ID to update (required).
-   **Remove null values** (optional, default: on): When enabled, blank or null field values are excluded from the update request instead of clearing the field in Pardot.
-   **Prospect fields** (optional): Map standard and custom fields to update. Custom fields are loaded dynamically from your Pardot account.

### `Action` Upsert Pardot prospect

Create or update a Pardot prospect matched by email address.

**Inputs**

-   **Pardot Business Unit**
-   **Email address**: Prospect email address (required).
-   **Prospect fields** (optional): Map standard and custom fields. Custom fields are loaded dynamically from your Pardot account.

## List actions

### `Action` Get Pardot list

Look up a Pardot list by ID or name.

**Inputs**

-   **Pardot Business Unit**
-   **List ID** (optional): Pardot list ID to look up.
-   **List name** (optional): Name of the list to look up (used if list ID is not provided).

### `Action` Create Pardot list

Create a new Pardot list.

**Inputs**

-   **Pardot Business Unit**
-   **List name**: Name of the list to create (required).
-   **Description** (optional): Description for the list.
-   **Is public** (optional): Whether the list is public.
-   **Folder ID** (optional): Folder ID to place the list in.

### `Action` Update Pardot list

Update an existing Pardot list.

**Inputs**

-   **Pardot Business Unit**
-   **List ID**: ID of the list to update (required).
-   **List name** (optional): New name for the list.
-   **Description** (optional): New description for the list.
-   **Is public** (optional): Whether the list is public.
-   **Folder ID** (optional): Folder ID to place the list in.

## List membership actions

### `Action` Add Pardot prospect to list

Add a prospect to a Pardot list.

**Inputs**

-   **Pardot Business Unit**
-   **Prospect ID**: Pardot prospect ID (required).
-   **List ID**: Pardot list ID (required).

### `Action` Remove Pardot prospect from list

Remove a prospect from a Pardot list by membership ID.

**Inputs**

-   **Pardot Business Unit**
-   **List membership ID**: Pardot list membership ID to remove (required).

### `Action` Look up Pardot list membership

Check if a prospect is a member of a Pardot list.

**Inputs**

-   **Pardot Business Unit**
-   **Prospect ID**: Pardot prospect ID (required).
-   **List ID**: Pardot list ID (required).

### Run settings

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))
