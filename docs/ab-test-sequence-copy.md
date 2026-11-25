---
title: A/B test your sequence copy
description: How to run A/B tests on campaign sequence copy, read split results, and promote the winning variant.
last_synced: 2026-11-17T21:04:11.108Z
---

# A/B test your sequence copy

Run two versions of your sequence copy against each other, then send the rest of your leads to whichever one performs better.

A sequence can hold two copy variants at once, and each lead that enrolls is assigned to one of them. Everything else stays shared — the same leads, sender accounts, schedule, and settings — so the only thing that differs between the two variants is the writing. A/B testing lives in the `Sequence` tab, alongside the rest of the editor.

For writing and personalizing the copy itself, see [Build your sequence](https://university.clay.com/docs/build-your-sequence).

## Creating a variant

1.  Open the `Sequence` tab and click `A/B test`. Clay adds a second variant called `Variant B`, splits enrollment 50/50 between the two, and opens the new variant's name for editing with the generated name selected — so you can call it something descriptive straight away, or leave it as `Variant B`.
2.  The new variant starts as an exact copy of the first, so nothing is under test yet. On the message you want to vary, click `Test subject` or `Test body`.
3.  Write the alternative copy in the field that unlocks. It's seeded with the original wording, so you're editing rather than starting from a blank message.
4.  Repeat for any other subject or body you want to vary. A test can cover one field of one message or every field of every message, with one exception: a message that replies on an existing thread inherits that thread's subject, so only its body can be tested.

Once a second variant exists, the same choice also lives in each message's 3-dot menu, as `A/B test subject` and `A/B test body` checkboxes. They're the same toggles, and they show you which of that message's fields are currently under test. Unchecking one hands the field back to the shared copy, and whatever you typed into it while it was under test is dropped.

Where the window is wide enough, both variants sit side by side. Otherwise the editor shows one at a time — use the variant name above it to switch between them, or to `Rename` a variant to something more descriptive than `Variant A` and `Variant B`.

### The shared sequence shape

Both variants always have the same number of messages, the same delay before each one, and the same reply-or-new-thread setting per message. Only subject and body text can differ, and Clay keeps that true for you rather than leaving it to be remembered: the structural controls in the editor write to both variants at once, so adding a message adds it to both.

That constraint is also what keeps the comparison meaningful. If one variant had an extra message or a longer gap before it, a difference in replies would be telling you about timing as much as about copy.

**Note:** A lead is enrolled only when it has the data every variant in the sequence needs, so a variable used in one variant applies to the whole sequence. It's worth checking field coverage for both variants before you launch, since a sparsely filled field will hold leads back whichever variant they would have drawn.

## Reading the results

Open the `Analytics` tab. While a test is running, two filters scope what you're looking at:

-   `Variant` scopes the whole view to the leads one variant enrolled.
-   `Compare` puts two variants in columns side by side over the same date range.

Each variant reports the same figures a sequence does, counted over its own leads.

| Section | Figures |
| --- | --- |
| Lead funnel | Processed, Enrolled, Complete, Paused |
| Variant statistics | Sent, Replies, Bounces, Unsubscribes |

Underneath those sits the number a test is usually decided on — reply rate, with the counts behind it: how many of the delivered emails drew a reply, and how many of those replies were positive. It's the share of delivered emails rather than of emails sent, so it reads a little higher here than the sequence-wide reply rate does on the same sequence. For that view and for reply categories, see [Campaign analytics and replies](https://university.clay.com/docs/campaign-analytics-and-replies).

### Give the data time to mature

Replies lag sends by days, so a variant that only started enrolling recently reads low for reasons that have nothing to do with its copy. Clay shows what share of a variant's sends are at least three days old, along with the reply rate among just those sends.

A difference is worth acting on once most of the sends in both columns are mature and the counts are big enough to mean something. Each column also names the window its variant was running in — `Live since` a date, or `Ran` between two — because two variants that never enrolled leads at the same time differ by when they ran as much as by how they were written.

## Converting the winner

When one variant is clearly ahead, end the test and promote it.

1.  Save any outstanding copy edits. Until you do, `End test` is disabled and hovering it reads `Save copy changes before choosing a winning variant.`, so the variants you decide between are the ones on file.
2.  Click `End test`.
3.  In the `Complete A/B test` dialog, choose the `Winning variant`. It opens with nothing selected, and confirming without a choice asks you to `Pick a variant to continue with.`
4.  Confirm with `Select winning variant`.

`Keep testing` closes the dialog and leaves the split as it was.

Promoting a winner is an allocation change rather than a copy edit, and it applies to future enrollments only:

-   Every lead that enrolls from then on gets the winner's copy, and the other variant leaves the editor.
-   Leads already enrolled keep the copy they were sent, and their emails play out as written.
-   The variant that lost keeps its results too: it stays available in the `Variant` and `Compare` filters, marked `Ended`.

There's nothing to configure about statistical significance, and no threshold Clay is waiting to cross. You have the rates, the counts behind them, and how mature the data is — the call is yours to make.

### Cancelling on a draft sequence

While the sequence is still `Draft`, the same button reads `Cancel test` and opens `Revert to one variant` instead. Pick the `Variant to keep`, and the other is dropped when you save. Nothing has enrolled, so there are no results to preserve.

If neither variant has any copy written yet, there is nothing to lose whichever one you keep, so Clay skips the dialog — `Cancel test` drops the second variant straight away.

## FAQs

### Can I change the copy once a test is running?

It depends on the sequence's status. Copy edits, adding or removing a variant, and changing the split each unlock at different points:

| Sequence status | Copy edits | Adding or removing a variant | Split |
| --- | --- | --- | --- |
| Draft | Saved in place | Yes | Editable in the editor |
| Active | Locked | No | Winner promotion only, and every change is recorded |
| Paused | Saved as a new variant, so its results stay separate from the copy it replaced | Yes | Editable in the editor |
| Completed | Locked | No | Locked |

Renaming a variant is available in every status.

### Is spintax the same as an A/B test?

No, and the two work well together. Spintax randomizes individual words and phrases inside one sequence's copy so that sends don't read identically, and Clay doesn't track which wording a given lead received. An A/B variant is a tracked arm with results of its own, and a sequence under test can still use spintax throughout.

### How does Clay decide which variant a lead gets?

Each lead is assigned when it enrolls and keeps that variant for the rest of the sequence. The assignment converges on the split you configured across the full lead set, so a single day's batch of enrollments can look uneven — a 60/40 result on a few hundred leads is normal, and it evens out as the rest of the segment enrolls.
