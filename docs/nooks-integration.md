---
title: Nooks integration
description: Enroll prospects in Nooks sequences and import prospect, account, and email data into Clay.
last_synced: 2026-08-06T02:10:13.778Z
---

# Nooks integration

Enroll prospects in Nooks sequences and import prospect, account, and email data into Clay.

Nooks is a sales engagement platform for running outbound sequences. With this integration, you can import prospects, accounts, and email activity from Nooks into Clay, then enroll prospects in Nooks sequences using messages written in Clay.

**Note:** The Nooks integration requires an Explorer plan or above.

## Creating a table with Nooks

1.  In a workbook, click `+ Add` at the bottom.
2.  Search for `Nooks` and select from the results.
3.  In the modal, you will be asked to `Select Nooks account`.
    -   If you haven't already connected your Nooks account, click `+ Add account` and enter your Nooks API key. API keys are scoped to a single Nooks workspace, so the account you connect determines which sequences, prospects, and mailboxes are available in Clay.

### `Source` Import prospects from Nooks

Import Nooks prospects into a table, with optional filters by sequence, account, email, and more.

**Inputs**

All filters are optional — leave them blank to import all prospects.

-   **Sequence:** Only return prospects enrolled in this sequence. Displays as a dropdown populated from your Nooks account, with private sequences labeled `(private)`.
-   **Account ID:** Only return prospects associated with this account.
-   **Primary emails:** List of email addresses to match (up to 10).
-   **Name:** Filter prospects by exact full-name match.
-   **Job title:** Filter prospects by exact job-title match.
-   **CRM ID:** Filter prospects by their external ID in your CRM.
-   **Prospect IDs:** List of specific Nooks prospect IDs to fetch. You can select these values from another table.
-   **Updated after:** Only return prospects updated on or after this date.
-   **Updated before:** Only return prospects updated before this date (exclusive).
-   **Limit:** The maximum number of prospects to import. The maximum is 50,000.

### `Source` Import accounts from Nooks

Import Nooks accounts (companies) into a table.

**Inputs**

All filters are optional — leave them blank to import all accounts.

-   **Company domain:** Filter accounts by exact domain match.
-   **Company name:** Filter accounts by exact name match.
-   **CRM ID:** Filter accounts by their external ID in your CRM.
-   **Account IDs:** List of specific Nooks account IDs to fetch. You can select these values from another table.
-   **Updated after:** Only return accounts updated on or after this date.
-   **Updated before:** Only return accounts updated before this date (exclusive).
-   **Limit:** The maximum number of accounts to import. The maximum is 50,000.

### `Source` Import emails from Nooks

Import emails sent from Nooks into a table, including delivery status and open and reply activity.

**Inputs**

All filters are optional — leave them blank to import all emails.

-   **Prospect ID:** Only return emails for this prospect.
-   **Account ID:** Only return emails associated with this account.
-   **Task ID:** Only return emails sent for this sequence task.
-   **Status:** Only return emails with one of the selected statuses — `Draft`, `In progress`, `Sent`, or `Failed`.
-   **Email IDs:** List of specific Nooks email IDs to fetch. You can select these values from another table.
-   **Updated after:** Only return emails updated on or after this date.
-   **Updated before:** Only return emails updated before this date (exclusive).
-   **Include related records:** Expand `Prospect`, `Sequence`, or `Sequence step` records inline instead of returning only their IDs.
-   **Limit:** The maximum number of emails to import. The maximum is 50,000.

## Enriching data with Nooks

1.  While in a Clay table, click `Add enrichment` and search for `Nooks`.
2.  Under `Integrations`, select one of the Nooks actions.
3.  In the modal, you will be asked to `Select Nooks account`.

**Note:** Sequences can't be created from Clay, so build them in Nooks first. The Sequence dropdown only lists sequences that are enabled in your Nooks workspace.

### `Action` Get prospect

Look up a Nooks prospect by prospect ID or primary email and return their details.

**Inputs**

Required:

-   **Prospect ID:** The ID of the Nooks prospect to look up. (Required if `Primary email` is not provided.)
-   **Primary email:** The primary email of the Nooks prospect to look up. (Required if `Prospect ID` is not provided.)

Provide exactly one identifier — the action fails if both fields are filled in.

**Outputs**

-   **Prospect ID:** The prospect's Nooks ID.
-   **Full name:** The prospect's full name.
-   **First name:** The prospect's first name.
-   **Last name:** The prospect's last name.
-   **Job title:** The prospect's job title.
-   **Primary email:** The prospect's primary email address.
-   **Social URL:** The prospect's professional profile URL.
-   **CRM ID:** The prospect's external ID in your CRM.
-   **Account ID:** The Nooks ID of the account the prospect belongs to.
-   **Created at:** When the prospect was created in Nooks.
-   **Updated at:** When the prospect was last updated in Nooks.

When a primary email matches more than one prospect, the action returns the matches instead of a single record:

-   **Matching prospect IDs:** The Nooks IDs of every prospect that matched the email.
-   **Matching prospects:** The full details of each matching prospect, including their ID, name, job title, primary email, social URL, CRM ID, account ID, and created and updated timestamps.
-   **Match count:** How many prospects matched the email.
-   **More matching prospects available:** Whether additional matches exist beyond those returned.

### `Action` Get account

Look up a single Nooks account (company) by ID.

**Inputs**

Required:

-   **Account ID:** The ID of the Nooks account (company) to look up.

**Outputs**

-   **Account ID:** The account's Nooks ID.
-   **Company name:** The name of the company.
-   **Company domain:** The company's domain.
-   **Employee count:** The number of employees at the company.
-   **Company professional profile URL:** The company's professional profile URL.
-   **Description:** A description of the company.
-   **Created at:** When the account was created in Nooks.
-   **Updated at:** When the account was last updated in Nooks.

### `Action` Get sequence state

Look up a single Nooks sequence state (enrollment) by ID, including its current state, sequence, prospect, account, and current step.

**Inputs**

Required:

-   **Sequence state ID:** The ID of the Nooks sequence state (enrollment) to look up.

Optional:

-   **Include related records:** Expand up to 3 related records inline instead of returning only their IDs. Choose from `Sequence`, `Prospect`, `Creator`, and `Current step`.

**Outputs**

-   **Sequence state ID:** The enrollment's Nooks ID.
-   **State:** The current state of the enrollment.
-   **Sequence ID:** The Nooks ID of the sequence.
-   **Prospect ID:** The Nooks ID of the enrolled prospect.
-   **Account ID:** The Nooks ID of the prospect's account.
-   **Current step ID:** The Nooks ID of the step the prospect is currently on.
-   **Creator ID:** The Nooks ID of the user who created the enrollment.
-   **Owner ID:** The Nooks ID of the user who owns the enrollment.
-   **Created at:** When the enrollment was created.
-   **Updated at:** When the enrollment was last updated.

### `Action` Enroll prospect in sequence

Enroll a Nooks prospect into a sequence.

**Inputs**

Required:

-   **Prospect ID:** The ID of the Nooks prospect to enroll. You can get this from an `Import prospects from Nooks` source or a `Get prospect` action.
-   **Sequence:** The sequence to enroll the prospect in. Displays as a dropdown populated from your Nooks account.
-   **Owner:** The Nooks user who will own this enrollment. Outreach is sent on this user's behalf.

Optional:

-   **Mailbox:** The mailbox to send email outreach from. Defaults to the owner's primary mailbox if left blank.
-   **Initial state:** Whether the enrollment starts `Active` or `Paused`. Defaults to `Active`.
-   **Scheduled start time:** When to start the sequence, as an ISO 8601 timestamp with a timezone offset (for example, `2025-12-01T09:00:00-05:00`). Starts immediately if left blank.
-   **Email overrides:** Replace the subject or body of individual email steps in the selected sequence.

**Outputs**

-   **Sequence state ID:** The Nooks ID of the enrollment that was created.
-   **State:** The state the enrollment was created in.
-   **Already enrolled:** Whether the prospect was already enrolled in this sequence.
-   **Prospect ID:** The Nooks ID of the enrolled prospect.
-   **Sequence ID:** The Nooks ID of the sequence.
-   **Current step ID:** The Nooks ID of the step the prospect starts on.
-   **Owner ID:** The Nooks ID of the enrollment's owner.
-   **Created at:** When the enrollment was created.
-   **Updated at:** When the enrollment was last updated.

### `Action` Remove prospect from sequence

Unenroll a prospect from a Nooks sequence by deleting the sequence state and cancelling pending tasks.

**Inputs**

Required:

-   **Sequence state ID:** The ID of the Nooks sequence state (enrollment) to remove.

**Outputs**

-   **Removed:** Whether the enrollment was removed.
-   **Sequence state ID:** The Nooks ID of the enrollment that was removed.

### `Action` Finish sequence state

Mark a Nooks sequence state as finished, stopping the prospect's progression through the sequence.

**Inputs**

Required:

-   **Sequence state ID:** The ID of the Nooks sequence state (enrollment) to mark as finished.

**Outputs**

-   **Finished:** Whether the enrollment was marked as finished.
-   **Sequence state ID:** The Nooks ID of the enrollment that was finished.

### Run settings

-   **Auto-update:** Recommended for `Enroll prospect in sequence` so that new rows added to Clay are automatically enrolled in Nooks.
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

## FAQs

### How many credits do the Nooks actions use?

Each Nooks action costs 1 credit per run. `Get prospect`, `Get account`, and `Get sequence state` refund that credit when the lookup finds no match, so unmatched rows don't cost you anything.

### What happens if the prospect is already enrolled in the sequence?

The run succeeds rather than erroring, and `Already enrolled` returns true. Nooks won't create a second enrollment, so re-running `Enroll prospect in sequence` across the same rows won't double-enroll anyone.

### Can I use messages written in Clay in a Nooks sequence?

Yes. After you select a sequence in `Enroll prospect in sequence`, every email step in that sequence loads as its own subject and body input under `Email overrides`, so you can map an AI-generated Clay column to each step. Nooks supports HTML and line breaks in these fields, and any override you leave empty falls back to the step's template in Nooks. Nooks is also available in Clay's `Send to sequencer` flow if you'd rather draft the full message sequence in Clay first.

### Why are some of my Nooks accounts missing from the imported table?

`Import accounts from Nooks` only returns accounts that Nooks sourced from a connected CRM, such as Salesforce or HubSpot. Accounts created directly in Nooks or brought in from another source won't appear.

### Do Nooks sources stay up to date?

Each Nooks source runs on a daily schedule by default and deduplicates on the record's Nooks ID, so scheduled runs update existing rows instead of appending duplicates.

### Why is my Nooks action retrying instead of returning data?

Nooks rate limits requests per workspace, and Clay automatically waits and retries when it hits that limit. Large imports and high-volume enrollment runs can take longer to finish as a result.

## Related

-   [Email sequencer](https://university.clay.com/docs/email-sequencer)
-   [Outreach integration](https://www.clay.com/university/guide/outreach-integration-overview)
-   [Salesloft](https://www.clay.com/university/guide/salesloft-integration-overview)
