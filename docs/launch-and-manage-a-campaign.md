---
title: Launch and manage a campaign
description: Set a campaign's schedule and credit budget, launch it, and pause, resume, or complete it as leads move through the sequence.
last_synced: 2026-11-17T20:59:00.070Z
---

# Launch and manage a campaign

Set a sequence's schedule, launch it, and manage sending as leads move through its steps.

A sequence is ready to launch once it has a lead list, at least one step, and at least one sender account. Launching starts sending on the schedule you've set and enrolls new leads as they arrive in your segment.

From there, managing a sequence comes down to three controls: pause it to make changes, resume when you're ready, and complete it once you've got what you need. For the reporting side once it's live, see [Campaign analytics and replies](https://university.clay.com/docs/campaign-analytics-and-replies).

## Schedule settings

A sequence's sending window lives in its settings: click the sequence's name at the top of the page and choose `Settings`. `Schedule` is the section at the top. Start with `Schedule type` — it sets the shape of the window, and only `Custom schedule` exposes the individual fields.

`Timezone` applies to every schedule type but `As fast as possible`, which hides the field. `Custom schedule` opens four more:

| Setting | What it does |
| --- | --- |
| Timezone | Sets the clock every other schedule field is read against. Defaults to America/New_York — pick the timezone your sending accounts would normally send from. |
| Send on days | Tick any combination of Mon through Sun. At least one day is required. |
| Start time and End time | The daily sending window. The start has to be earlier than the end. |
| Min time between emails (min) | The minimum gap Clay leaves between two sends. Accepts 3 to 30 minutes, and defaults to 20. |
| Sequence start date (optional) | If set, a launched sequence only starts sending on that day. Leave it blank and sending starts as soon as you launch. |

**Note:** Picking `Optimized for deliverability` or `As fast as possible` overwrites the day, time, and gap fields with that type's preset values, and clears `Sequence start date (optional)`. Switching back to `Custom schedule` keeps those preset values rather than restoring what you had before, so re-enter your own settings after a round trip.

### Daily sending capacity

As you change these fields, the line above them updates with what the schedule adds up to — `Expected to finish in` a number of days, alongside how many emails per day your selected sender accounts can send between them. Sequences fed lead by lead from a workflow have no lead total to project against, so they show `Sending capacity` instead.

`Max new leads per day` caps how many new leads the sequence contacts each day, whichever schedule type you've picked. It defaults to 100,000 and limits new leads only, not follow-ups to leads already in the sequence. Daily volume comes from the sender accounts you've selected and their individual send limits, which is why selecting several accounts is what makes a sequence move faster.

One setting does shape how that capacity gets spent. `Follow-up percentage`, further down in `Settings`, sets the share of emails allocated to follow-ups for leads already in the sequence before Clay reaches out to new ones.

## Launching

When the sequence is ready, click `Launch sequence` at the top of the sequence page.

1.  Clay checks the sequence. If anything's missing, it takes you to the tab that needs attention with the field flagged.
2.  The `Launch sequence` modal opens. It confirms how many leads the sequence includes, flags a warning if the spam check graded your copy poorly, and shows the `Estimated total cost` in action credits and data credits. A sequence fed by a workflow has no lead total to price against, so it shows `Estimated cost per lead` in place of a total.
3.  Click `Confirm and launch` to start sending.

The checks that have to pass are:

-   `Sequence name is required`.
-   `Add a lead list` — the audience segment supplying leads. Sequences fed by a workflow don't need one. [Get leads ready to sequence](https://university.clay.com/docs/get-leads-ready-to-sequence) covers building that segment.
-   `Add at least one sequence step`.
-   `Message body is required`, and `Subject is required for new threads`, for every step in every variant.
-   `Add at least one sender account`.
-   `Select a sender field or set assignment to none` — only when you've set up per-lead sender assignment.

### What launch locks

Launching fixes the shape of the sequence. The number of steps and their order are set for its whole life, because emails already rendered and sent are tied to that structure — so a sequence you might want to run with five steps instead of three is a new sequence rather than an edit to this one. [Build your sequence](https://university.clay.com/docs/build-your-sequence) is where that structure gets set in the first place.

Everything else reopens when you pause. Message copy, subject lines, the wait between steps, sender accounts, and schedule settings are all editable in `Paused`, and your changes apply to the leads that haven't been sequenced yet.

**Note:** The audience field supplying each lead's email address is the one setting that stays locked after launch, in `Paused` too. Leads already enrolled were deduplicated and sent against that field, so switching it would quietly retarget the ones still queued. Set it before you launch.

## What happens to an enrolled lead

Enrollment is the moment a lead's copy gets written. Clay reads that lead's fields from Audiences, renders every step of the sequence — variables, AI snippets, spintax, conditional blocks — and hands the finished emails to the sending infrastructure. From then on, that lead's messages are fixed.

That's what makes post-launch edits apply only to leads that haven't been sequenced yet: rewrite step 3 while the sequence is paused, and leads enrolled after you resume get the new copy, while leads already enrolled keep the version generated for them. It also means a lead's data is a snapshot taken at enrollment — a field that fills in later, or a value that changes in Audiences, won't rewrite an email that's already been rendered, so it's worth checking that a segment is enriched the way you want before you sequence it.

From there, an enrolled lead:

-   Runs to the end of the sequence if it's left alone.
-   Stops early when the lead replies. An out-of-office auto-reply is recognized as such, so it doesn't end the lead's sequence the way a genuine reply does.
-   Stays in the sequence for good. You can pause it, and pausing is how you stop sending to someone, but you can't remove it.

## Pause, resume, and complete

The controls for a launched sequence sit in the same place as `Launch sequence` did, at the top of the sequence page. Which ones you see depends on where the sequence is in its lifecycle, shown as a badge next to its name.

| State | What you can do | What’s happening |
| --- | --- | --- |
| Draft | Configure everything — steps, leads, senders, schedule, settings. Send test emails once the sequence is valid. | Nothing is sending. |
| Active | Monitor Analytics, Activity, and Replies. Pause to make changes, or complete the sequence. | Emails are going out on schedule, and new leads are enrolled as they arrive. |
| Paused | Edit copy, senders, schedule, and settings, then resume or complete. Sequence steps can’t be added, removed, or reordered. | Sending has stopped. Lead data and statuses are preserved. |
| Completed | View Analytics, Activity, and Replies. | The sequence has ended permanently. No new leads are enrolled and no further emails go out. |

Three controls move a sequence between those states. Each one opens a confirmation modal you have to confirm — `Pause sequence`, `Resume sequence`, or `Complete sequence` — so a sequence never changes state on a single click.

| Control | What it does |
| --- | --- |
| Pause | Stops new emails going out. Leads already in progress finish their current step, and everything else waits until you resume. Pausing is also how you get back into a sequence — it’s the state where copy, senders, schedule, and settings become editable again. |
| Resume | Starts sending again. New leads get sequenced, and paused leads continue from where they left off. |
| Complete | Ends the sequence permanently, and it can’t be undone. Leads still in the sequence stop receiving emails and no new leads are enrolled. Analytics, Activity, and Replies all stay available afterwards. |

**Note:** Edits you make while a sequence is paused need `Save` before they take effect. `Save` sits alongside the status buttons and only lights up when there are unsaved changes, so it doubles as a quick check on whether anything is still pending.

## Pausing an individual lead

Pausing works at the lead level too, independently of the sequence around it. A paused lead in an `Active` sequence stops receiving the rest of its emails while every other lead keeps going. The way to pause one person is through the segment feeding the sequence: take them out of it, and Clay pauses them in the sequence for you. That happens as long as `Pause lead on segment exit` is on, which it is by default.

A pause doesn't undo a lead's progress. Clay records it as a flag alongside the lead's position in the sequence, so resuming picks up at the next step rather than starting the sequence over. The pause is written to the lead's feed on the `Activity` tab as `Paused`, and you can filter the feed down to it with the `Lead status` filter.

Audience-based sequences don't have a `Leads` tab — lead-level detail lives on `Activity`, which has a lead rail with `Search leads` for finding one person and `View all leads` for getting back to the full feed.

### Automatic pauses

Two settings under `Settings` → `Enrollment` pause leads for you:

-   `Pause lead on segment exit`: pauses a lead in this sequence when they leave the segment. It's on by default — when someone stops matching the segment feeding the sequence, the rest of the emails don't go out to a lead who no longer belongs in it.
-   `Pause leads at the same company on reply`: when a lead replies, pauses other leads with the same email domain. Useful when you're sequencing several people at one account and want the conversation to happen once.

**Note:** `Pause lead on segment exit` only appears on sequences fed by a segment. A sequence that receives its leads from a workflow has no segment to leave, so the setting isn't shown.

## FAQs

### Does relaunching a sequence charge credits again?

Credits are charged when a lead is enrolled, and a lead that's already been sequenced isn't enrolled a second time. Pausing and resuming therefore doesn't re-charge for the leads already in the sequence.

New leads arriving in the segment after you resume are charged as they enroll, at 1 action credit per lead plus any data credits your AI snippets use.

### Can I reuse a sequence after completing it?

`Completed` is a final state. A completed sequence can't be moved back to `Active` and won't enroll new leads, so reaching those people again means building a new sequence and pointing it at the segment you want.

Renaming is allowed in every state, including `Completed`, so it's worth retitling a finished sequence with something you'll recognize later once it's sitting in the list next to its replacement.
