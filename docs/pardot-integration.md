---
title: Pardot integration
description: Manage Pardot prospects, lists, and list memberships from Clay using your existing Salesforce connection.
last_synced: 2026-07-01T00:00:00.000Z
---

# Pardot integration

Manage Pardot prospects, lists, and list memberships from Clay using your existing Salesforce connection.

Pardot (now Salesforce Marketing Cloud Account Engagement) is a B2B marketing automation platform. The Clay integration lets you create and update prospects, manage lists, and control list memberships — including custom prospect fields — without leaving your Clay table.

> **Note:** The Pardot integration is currently in closed beta. To request access, contact your account team or reach out in [#team-enterprise-and-billing](https://clay-hq.slack.com/archives/C08K72PDRBP).

## Connecting to Pardot

The Pardot integration authenticates through your existing Salesforce connection — no separate Pardot credential is required.

1.  In the home sidebar, click `Settings` → `Connections`.
2.  Confirm you have an active Salesforce connection. If not, click `Add connection`, search for `Salesforce`, and authenticate.
3.  When setting up a Pardot action, select your Salesforce account and then choose your **Pardot Business Unit** from the dropdown.

## Setting up the Pardot integration

1.  While in a Clay table, click `Add enrichment` and search for `Pardot`.
2.  Under `Integrations`, select the Pardot action you want to use.
3.  Select your Salesforce account, then choose the **Pardot Business Unit** you want to operate on.

## Actions

### Prospect actions

**`Action` Upsert Pardot prospect**

Create a prospect or update an existing one, matched by email address. This is the recommended action for syncing records from Clay to Pardot — it handles both new and returning prospects in a single step.

**Inputs**

-   **Pardot Business Unit**
-   **Email address**: Used to identify the prospect. Required.
-   **Prospect fields**: Standard and custom prospect fields populated dynamically from your Pardot account (e.g. first name, last name, company, job title, phone).

---

**`Action` Create Pardot prospect**

Create a new Pardot prospect.

**Inputs**

-   **Pardot Business Unit**
-   **Email address**
-   **Prospect fields**: Standard and custom fields, surfaced dynamically.

---

**`Action` Update Pardot prospect**

Update an existing Pardot prospect by email address.

**Inputs**

-   **Pardot Business Unit**
-   **Email address**
-   **Prospect fields**: Standard and custom fields to update, surfaced dynamically.

---

**`Action` Lookup Pardot prospect**

Retrieve a Pardot prospect record by email address.

**Inputs**

-   **Pardot Business Unit**
-   **Email address**

### List actions

**`Action` Get Pardot list**

Retrieve details for a Pardot list.

**Inputs**

-   **Pardot Business Unit**
-   **List ID**

---

**`Action` Create Pardot list**

Create a new Pardot list.

**Inputs**

-   **Pardot Business Unit**
-   **List name** and other list properties.

---

**`Action` Update Pardot list**

Update an existing Pardot list.

**Inputs**

-   **Pardot Business Unit**
-   **List ID**
-   **List properties to update**

### List membership actions

**`Action` Create Pardot list membership**

Add a prospect to a Pardot list.

**Inputs**

-   **Pardot Business Unit**
-   **List ID**
-   **Prospect ID** or **Email address**

---

**`Action` Lookup Pardot list membership**

Check whether a prospect is a member of a given list.

**Inputs**

-   **Pardot Business Unit**
-   **List ID**
-   **Prospect ID** or **Email address**

---

**`Action` Delete Pardot list membership**

Remove a prospect from a Pardot list.

**Inputs**

-   **Pardot Business Unit**
-   **List ID**
-   **Prospect ID** or **Email address**

## Custom prospect fields

All prospect actions (upsert, create, update) dynamically fetch the custom fields defined in your Pardot account. When you set up the action, the **Prospect fields** input shows both standard Pardot fields and any custom fields you've created in Pardot — no manual configuration required.
