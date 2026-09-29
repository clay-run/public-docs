---
title: Nooks integration
description: Enroll prospects in Nooks sequences and manage enrollment data directly from Clay tables.
last_synced: 2026-09-29T00:00:00.000Z
---

# Nooks integration

Enroll prospects in Nooks sequences and manage enrollment data directly from Clay tables.

Nooks is an AI-powered sales sequencer. With this integration you can enroll prospects into Nooks sequences directly from Clay, manage sequence states, and look up prospect and account records. Source actions for importing lists of prospects, emails, and accounts into Clay tables are currently in beta.

## Using Nooks in Clay

1.  While in a Clay table, click `Add enrichment` and search for `Nooks`.
2.  Under `Integrations`, select one of the Nooks actions.
3.  In the modal, you will be asked to `Select Nooks account`.
    -   Click `+ Add account` and enter your Nooks API key.

### `Action` Enroll prospect in sequence

Enroll a Nooks prospect into a sequence, with optional mailbox, scheduled start, paused state, and per-step email overrides.

**Inputs**

-   **Prospect ID (Required):** Obtain from an Import Prospects source or Get Prospect action.
-   **Sequence (Required):** Select from the dropdown of enabled Nooks sequences.
-   **Owner (Required):** The Nooks user who will own this enrollment. Outreach is sent on this user's behalf.

### `Action` Get sequence state

Look up a single Nooks sequence state (enrollment) by ID, including its current state, sequence, prospect, account, and current step.

**Inputs**

-   **Sequence state ID (Required)**

### `Action` Remove prospect from sequence

Unenroll a prospect from a Nooks sequence by deleting the sequence state and cancelling pending tasks.

**Inputs**

-   **Sequence state ID (Required)**

### `Action` Finish sequence state

Mark a Nooks sequence state as finished, stopping the prospect's progression through the sequence. This action is idempotent.

**Inputs**

-   **Sequence state ID (Required)**

### `Action` Get prospect

Look up a Nooks prospect by prospect ID or primary email and return their details.

**Inputs**

-   **Prospect ID** or **Email** (at least one required)

### `Action` Get account

Look up a single Nooks account (company) by ID — returns name, domain, employee count, professional URL, and description.

**Inputs**

-   **Account ID (Required)**

### `Action` Get user

Look up a Nooks user by email or CRM user ID and return their Nooks user ID.

**Inputs**

-   **Email** or **CRM user ID** (at least one required)

### `Source` Import prospects

Import a list of Nooks prospects into a table, with optional filters by sequence, account, email, and more.

**Currently in beta — contact support to enable.**

### `Source` Import emails

Import a list of emails sent from Nooks into a table, including delivery status, opens, clicks, bounces, and replies.

**Currently in beta — contact support to enable.**

### `Source` Import accounts

Import a list of Nooks accounts (companies) into a table. Results are restricted to accounts sourced from a connected CRM (Salesforce or HubSpot).

**Currently in beta — contact support to enable.**
