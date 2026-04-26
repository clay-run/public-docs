---
title: Outreach integration
source_url: https://university.clay.com/docs/outreach-integration-overview
description: AI-powered sales platform.
last_synced: 2026-04-26T01:40:27.028Z
upstream_hash: 0d1f6e673d3cff97157f154936c43bef311b4e51af40545f8c74555485ef76b0
---

# Outreach integration

AI-powered sales platform.

Outreach is a sales engagement platform that helps sales teams automate and optimize their outreach campaigns.

With this integration, you can create and update prospects, look up existing prospect data, add prospects to sequences, and find mailbox IDs in Outreach directly from Clay.

## Enriching data with Outreach

1.  While in a Clay table, click `Add enrichment` and search for `Outreach`.
2.  Under `Integrations`, select one of the Outreach options.
3.  In the modal, you will be asked to `Select Outreach account`.
    -   If you haven't already connected your Outreach account, click `+ Add account` and go through authentication.

### `Action` Update prospect

Use this action to update existing prospect records in Outreach.

-   **ID**
-   **Email**
-   **Basic information like name, company, title, etc. (Optional)**
-   **Address information (Optional)**
-   **Contact preferences (Optional)**
-   **Social media & websites (Optional)**
-   **Additional phone numbers (Optional)**
-   **Campaign & source information like tags, campaign name, event name, etc. (Optional)**
-   **Personal details like date of birth, gender, graduation date, etc. (Optional)**

### `Action` Create prospect

Use this action to create new prospect records in Outreach.

**Inputs**

-   **Email**
-   **Basic information like name, company, title, etc. (Optional)**
-   **Address information (Optional)**
-   **Contact preferences (Optional)**
-   **Social media & websites (Optional)**
-   **Additional phone numbers (Optional)**
-   **Campaign & source information like tags, campaign name, event name, etc. (Optional)**
-   **Personal details like date of birth, gender, graduation date, etc. (Optional)**

### Sending emails with `Create prospect`

When using this action, you may want to send emails to your new prospects. You can do this by adding email templates to your table and sending them with custom field inputs.

### `Action` Lookup prospect

Use this action to find and retrieve existing prospect data from Outreach.

**Inputs**

-   **Email (Optional)**
-   **Prospect ID (Optional)**
-   **Include Sequences (Optional)**

### `Action` Add to sequence

Use this action to add prospects to an Outreach sequence.

_Note: Sequences must be "Active" in Outreach for a lead to be successfully added._

**Inputs**

-   **Prospect ID**
-   **Sequence ID**
-   **Mailbox ID**

### `Action` Lookup mailbox by email address

Find the mailbox ID for a given email address in Outreach.

**Inputs**

-   **Email address**

## OAuth scopes

When connecting your Outreach account, Clay uses optional OAuth scopes to give you fine-grained control over permissions. Learn more about [optional scopes](https://university.clay.com/docs/oauth-optional-scopes).

### Required scopes

These permissions cannot be disabled and are always requested:

-   `users.all` — Read and write all users.
-   `stages.all` — Read and write all stages.
-   `sequenceSteps.all` — Read and write all sequence steps.
-   `sequenceStates.all` — Read and write all sequence states.
-   `sequences.all` — Read and write all sequences.
-   `roles.all` — Read and write all roles.
-   `recipients.all` — Read and write all recipients.
-   `prospects.all` — Read and write all prospects.
-   `opportunityStages.all` — Read and write all opportunity stages.
-   `opportunities.all` — Read and write all opportunities.
-   `mailboxes.all` — Read and write all mailboxes.
-   `events.all` — Read and write all events.

### Optional scopes (enabled by default)

These permissions are requested by default but can be disabled:

-   `tasks.all` — Read and write all tasks.
-   [`taskDispositions.read`](http://taskDispositions.read) — Read all task dispositions.
-   [`taskPriorities.read`](http://taskPriorities.read) — Read all task priorities.
-   [`taskPurposes.read`](http://taskPurposes.read) — Read all task purposes.

### Run settings

-   `Auto-update`
-   `Only run if:` The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))
