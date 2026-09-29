---
title: Nooks integration
description: Import accounts, prospects, and email activity from Nooks, enroll and manage prospects in sequences, and sync data between Clay and your Nooks workspace.
last_synced: 2026-09-29T00:00:00.000Z
---

# Nooks integration

Import accounts, prospects, and email activity from Nooks, enroll and manage prospects in sequences, and sync data between Clay and your Nooks workspace.

Nooks is a sales engagement platform that combines a parallel dialer with AI-powered prospecting and sequence management. Use the Nooks integration in Clay to pull your Nooks accounts, prospects, and email activity into Clay tables, enrich them alongside other data sources, and push contacts back into Nooks sequences. Nooks requires your own API key.

## Connecting Nooks in Clay

1. While in a Clay table, click `Add enrichment` and search for `Nooks`.
2. Under `Integrations`, select the Nooks action you want to use.
3. Click `+ Add account` and enter your Nooks API key to authenticate.

## Sources

The Nooks sources import data from your Nooks workspace into Clay tables. These sources are available for workspaces with Nooks sources enabled — contact Clay support to request access.

### `Source` Import accounts

Import your Nooks accounts as rows in a Clay table. Each imported row includes the account ID, name, domain, and other account attributes.

### `Source` Import prospects

Import your Nooks prospects as rows in a Clay table. Each imported row includes the prospect ID, name, email, sequence state, and other prospect attributes.

### `Source` Import emails

Import email activity records from your Nooks workspace as rows in a Clay table.

## Enrichment actions

### `Action` Get account

Look up a Nooks account by account ID and return its details.

**Inputs**

- **Account ID (Required):** The Nooks account ID to look up.

**Output**

Returns account name, domain, owner, and other account profile fields.

### `Action` Get prospect

Look up a Nooks prospect by prospect ID or primary email.

**Inputs**

Provide exactly one of:
- **Prospect ID:** The Nooks prospect ID.
- **Primary email:** The primary email address of the prospect.

**Output**

Returns prospect name, email, title, company, sequence state, and other prospect fields.

### `Action` Get user

Look up a Nooks user by email or CRM user ID and return their Nooks user ID.

**Inputs**

- **Email** or **CRM user ID** to identify the user.

**Output**

Returns the Nooks user ID and other user profile fields.

### `Action` Get sequence state

Return the sequence state for a specific prospect in a Nooks sequence.

**Inputs**

- **Prospect ID (Required):** The Nooks prospect ID.
- **Sequence ID:** The sequence to check the state for.

**Output**

Returns the sequence state details including status, current step, and timestamps.

### `Action` Enroll prospect in sequence

Enroll a Nooks prospect in a sequence.

**Inputs**

- **Prospect ID (Required):** The ID of the Nooks prospect to enroll. Obtain this from the Import Prospects source or Get Prospect action.
- **Sequence (Required):** The sequence to enroll the prospect in. Select from your active Nooks sequences.

Additional optional inputs control enrollment settings such as email step assignment and priority.

**Output**

Returns confirmation of the enrollment and the resulting sequence state.

### `Action` Remove prospect from sequence

Remove a Nooks prospect from a sequence.

**Inputs**

- **Prospect ID (Required):** The ID of the Nooks prospect to remove.
- **Sequence ID (Required):** The sequence to remove the prospect from.

**Output**

Returns confirmation of the removal.

### `Action` Finish sequence state

Mark a sequence state as finished for a Nooks prospect.

**Inputs**

- **Sequence state ID (Required):** The ID of the sequence state to finish.

**Output**

Returns the updated sequence state with finished status.
