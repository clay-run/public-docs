---
title: Troubleshooting the Outreach "Add to sequence" action
description: Resolve common errors when adding prospects to Outreach sequences from Clay.
last_synced: 2026-07-27T00:00:00.000Z
---

# Troubleshooting the Outreach "Add to sequence" action

When you use the Outreach [`Add to sequence`](https://university.clay.com/docs/outreach-integration-overview) action in Clay, some prospects may fail to enroll and return an error instead. These errors come directly from Outreach and reflect rules Outreach enforces on sequence enrollment.

This guide explains the most common errors, why they happen, and how to resolve them.

_The short version: all of these are enforced by Outreach, so you'll need to handle them in Outreach first:_

1.  For prospects in **exclusive sequences**, either remove them from the current sequence or change the sequence settings to non-exclusive.
2.  For prospects **already enrolled in this sequence**, check your Outreach settings to allow re-enrollment if needed.
3.  For the **locked user** error, verify the mailbox owner's Outreach permissions and account status.

Once you've made the fix in Outreach, re-run the `Add to sequence` action in Clay.

## Quick reference

| Error message | What it means | Where to fix it |
| --- | --- | --- |
| Prospect active in another exclusive sequence | The prospect is already enrolled in a sequence marked *exclusive* | Outreach |
| Prospect has already been in this sequence | The prospect was previously enrolled in this exact sequence | Outreach |
| User is locked | The mailbox owner's Outreach account is locked | Outreach admin |
| User not the owner | The mailbox owner can't add prospects to this sequence | Outreach admin / sequence settings |

## "Prospect active in another exclusive sequence"

### What it means

The prospect is already active in a different sequence that has been marked as **exclusive** in Outreach. Outreach does not allow a prospect to be in more than one exclusive sequence at a time, so the new enrollment is rejected.

### Why it happens

Sequences in Outreach can be flagged as exclusive to prevent a prospect from receiving overlapping outreach. Once a prospect is active in an exclusive sequence, any attempt to add them to another sequence fails until they finish or are removed from the first one.

### How to resolve it

Handle this in Outreach first, then re-run the `Add to sequence` action in Clay. You have two options:

-   **Remove the prospect from the current sequence.** Once they're no longer active in the exclusive sequence, they can be added to the new one.
-   **Change the sequence settings to non-exclusive.** If overlapping outreach is acceptable for your use case, an Outreach admin can turn off exclusivity so prospects can be enrolled in more than one sequence at a time.

_Tip: To avoid these failures upfront, add a condition in Clay to skip prospects who are currently active in another sequence._

## "Prospect has already been in this sequence"

### What it means

The prospect was **previously enrolled in this same sequence**. Outreach blocks re-adding a prospect to a sequence they've already been through, to avoid duplicate outreach.

### Why it happens

Outreach tracks each prospect's sequence history. By default, a prospect who has already been added to a specific sequence — whether they completed it, were finished early, or were removed — cannot be added to that same sequence again.

### How to resolve it

Handle this in Outreach first, then re-run the `Add to sequence` action in Clay:

-   **Check your Outreach settings to allow re-enrollment.** If you want the prospect to go through this sequence again, an Outreach admin can enable re-enrollment for the sequence so previously enrolled prospects become eligible.
-   **Or choose a different sequence.** If re-enrollment isn't appropriate, enroll the prospect in a new or follow-up sequence instead of the original one.

_Tip: If your table may contain prospects who were already run through this sequence, filter or dedupe them before the `Add to sequence` step._

## "User is locked" and "User not the owner"

Both of these errors relate to the **mailbox owner** used for enrollment. When you add a prospect to a sequence, Outreach associates the enrollment with a mailbox/user, and that user must be active and permitted to add prospects to the sequence. The error message will reference the specific mailbox ID involved.

### How to resolve it

For both errors, **verify the mailbox owner's Outreach permissions and account status.** An Outreach admin should confirm the following for the user tied to the mailbox in the error:

-   **The account is not locked.** Locked users can't perform actions in Outreach, including adding prospects to sequences — unlock the user if needed.
-   **The mailbox is active and properly connected.** Mailboxes can be disabled or disconnected due to authentication or sync issues.
-   **The user is permitted to add prospects to this sequence.** Some sequences restrict enrollment to the sequence owner or users with sufficient permissions. Either use a mailbox whose user owns or has access to the sequence, or adjust the sequence's sharing settings so the mailbox owner is authorized to enroll prospects.

Once the account is unlocked and permissions are confirmed, re-run the `Add to sequence` action in Clay.

_Tip: Use the [`Lookup mailbox by email address`](https://university.clay.com/docs/outreach-integration-overview) action to confirm you're passing the correct mailbox ID for an authorized user._

## General tips

-   **These errors originate in Outreach, not Clay.** Clay passes the enrollment request to Outreach and surfaces whatever Outreach returns. Most fixes happen in your Outreach settings, permissions, or sequence configuration.
-   **Sequences must be "Active" in Outreach** for a prospect to be successfully added.
-   **Check the mailbox owner first.** Many enrollment failures trace back to the user/mailbox being used. Confirm it's active, unlocked, and authorized before troubleshooting further.
-   **Re-run after fixing.** Once you've resolved the underlying issue in Outreach, re-run the `Add to sequence` action on the affected prospects in Clay.
-   **Filter proactively.** Where possible, add conditions in Clay to skip prospects that are likely to fail (e.g., already in an exclusive sequence, or previously enrolled) so your runs stay clean.
