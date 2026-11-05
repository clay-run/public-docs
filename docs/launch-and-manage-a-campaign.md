---
title: Launch and manage a campaign
description: How to set a campaign's schedule and credit budget, launch it, and manage sending through pause, resume, and complete controls as leads move through the sequence.
last_synced: 2026-09-01T03:19:07.322Z
---

# Launch and manage a campaign

Set a campaign's schedule and credit budget, launch it, and manage sending as leads move through the sequence.

A campaign is ready to launch once it has a lead list, at least one sequence step, and at least one sender account. Launching starts sending on the schedule you've set and enrolls new leads as they arrive in your segment.

From there, managing a campaign comes down to three controls: pause it to make changes, resume when you're ready, and complete it once you've got what you need. For the reporting side once it's live, see [Campaign analytics and replies](https://university.clay.com/docs/campaign-analytics-and-replies).

## Schedule settings

A campaign's sending window lives on the `Settings` tab, in the `Schedule` section at the top. Start with `Schedule type` — it sets the shape of the window, and only `Custom schedule` exposes the individual fields.

`Timezone` applies to every schedule type but `Send immediately`, which hides the field. `Custom schedule` opens four more:

| Setting | What it does |
| --- | --- |
| Timezone | Sets the clock every other schedule field is read against. Defaults to America/New_York — pick the timezone your sending accounts would normally send from. |
| Send on days | Tick any combination of Mon through Sun. At least one day is required. |
| Start time and End time | The daily sending window. The start has to be earlier than the end. |
| Min time between emails (min) | The minimum gap Clay leaves between two sends. Accepts 3 to 30 minutes, and defaults to 20. |
| Campaign start date (optional) | If set, a launched campaign only starts sending on that day. Leave it blank and sending starts as soon as you launch. |

**Note:** Picking `Optimized for deliverability` or `Send immediately` overwrites the day, time, and gap fields with that type's preset values, and clears `Campaign start date (optional)`. Switching back to `Custom schedule` keeps those preset values rather than restoring what you had before, so re-enter your own settings after a round trip.

### Daily sending capacity

As you change these fields, the line above them updates with what the schedule adds up to — `Expected to finish in` a number of days, alongside how many emails per day your selected sender accounts can send between them. Campaigns fed lead by lead from a workflow have no lead total to project against, so they show `Sending capacity` instead.

There's no per-campaign cap you can set on how many new leads enter the sequence each day. Clay does apply a platform-wide ceiling on how many leads begin a sequence in a single day, and it sits far above what a realistic campaign reaches — it isn't a field anywhere in the product. Daily volume comes from the sender accounts you've selected and their individual send limits, which is why selecting several accounts is what makes a campaign move faster.

One setting does shape how that capacity gets spent. `Follow-up percentage`, further down the `Settings` tab, sets the share of emails allocated to follow-ups for leads already in the sequence before Clay reaches out to new ones.

## Setting a credit budget

A credit budget caps what a campaign is allowed to spend. Budgets live at the workspace level rather than on a single campaign, so one budget can cover several campaigns alongside other work in the workspace. To create one:

1.  Open workspace settings and go to `Budgets`.
2.  Click `Create`.
3.  Give the budget a `Budget name` and set its `Credit limit`.
4.  Choose a `Reset frequency`, if the field is shown for your workspace — `Never`, `Monthly`, `Quarterly`, or `Annual`. A resetting budget renews to its full limit on the 1st of each period.
5.  Set `Access settings` to control who can create workflows using the budget — either `Anyone in the workspace`, or `Specific people and groups`.
6.  Click `Create budget` to save it.

### Attaching and tracking a budget

You attach a budget to a campaign at launch, from the `Budget` select in the `Launch campaign` modal. If your workspace has budgets you can access, choosing one is required — `Confirm and launch` stays disabled until you do. The `Resume campaign` modal offers the same select, so resuming is also your chance to move a campaign onto a different budget.

Each budget shows how much room is left next to its name: `Less than 10% remaining` as it gets close, and `Limit reached` once it's spent. Clay emails the budget's alert recipients at both points, so nobody has to watch the number.

When a budget hits its limit, campaigns drawing on it stop spending credits, which stops new leads enrolling. Raising the limit, waiting for the next reset, or moving the campaign onto a budget with room all get it going again.

**Note:** The `Budget` select lists the budgets you have access to. If a colleague assigned a budget you can't otherwise see, it still appears by name so you can tell which budget the campaign is drawing from.

## Launching

When the campaign is ready, click `Launch campaign` at the top of the campaign page.

1.  Clay checks the campaign. If anything's missing, it takes you to the tab that needs attention with the field flagged.
2.  The `Launch campaign` modal opens. It confirms how many leads the campaign includes, flags a warning if the spam check graded your copy poorly, and shows the `Estimated total cost` in action credits and data credits. A campaign fed by a workflow has no lead total to price against, so it shows `Estimated cost per lead` in place of a total.
3.  Click `Confirm and launch` to start sending.

The checks that have to pass are:

-   `Campaign name is required`.
-   `Add a lead list` — the audience segment supplying leads. Campaigns fed by a workflow don't need one. [Get leads ready to sequence](https://university.clay.com/docs/get-leads-ready-to-sequence) covers building that segment.
-   `Add at least one sequence step`.
-   `Message body is required`, and `Subject is required for new threads`, for every step in every variant.
-   `Add at least one sender account`.
-   `Select a sender field or set assignment to none` — only when you've set up per-lead sender assignment.

### What launch locks

Launching fixes the shape of the sequence. The number of steps and their order are set for the life of the campaign, because emails already rendered and sent are tied to that structure — so a campaign you might want to run with five steps instead of three is a new campaign rather than an edit to this one. [Build your sequence](https://university.clay.com/docs/build-your-sequence) is where that structure gets set in the first place.

Everything else reopens when you pause. Message copy, subject lines, the wait between steps, sender accounts, and schedule settings are all editable in `Paused`, and your changes apply to the leads that haven't been sequenced yet.

**Note:** The audience field supplying each lead's email address is the one setting that stays locked after launch, in `Paused` too. Leads already enrolled were deduplicated and sent against that field, so switching it would quietly retarget the ones still queued. Set it before you launch.

## What happens to an enrolled lead

Enrollment is the moment a lead's copy gets written. Clay reads that lead's fields from Audiences, renders every step of the sequence — variables, AI snippets, spintax, conditional blocks — and hands the finished emails to the sending infrastructure. From then on, that lead's messages are fixed.

That's what makes post-launch edits apply only to leads that haven't been sequenced yet: rewrite step 3 while the campaign is paused, and leads enrolled after you resume get the new copy, while leads already enrolled keep the version generated for them. It also means a lead's data is a snapshot taken at enrollment — a field that fills in later, or a value that changes in Audiences, won't rewrite an email that's already been rendered, so it's worth checking that a segment is enriched the way you want before you sequence it.

From there, an enrolled lead:

-   Runs to the end of the sequence if it's left alone.
-   Stops early when the lead replies. An out-of-office auto-reply is recognized as such, so it doesn't end the lead's sequence the way a genuine reply does.
-   Stays in the campaign for good. You can pause it, and pausing is how you stop sending to someone, but you can't remove it.

## Pause, resume, and complete

The controls for a launched campaign sit in the same place as `Launch campaign` did, at the top of the campaign page. Which ones you see depends on where the campaign is in its lifecycle, shown as a badge next to its name.

| State | What you can do | What's happening |
| --- | --- | --- |
| Draft | Configure everything — sequence, leads, senders, schedule, settings. Send test emails once the campaign is valid. | Nothing is sending. |
| Active | Monitor Analytics, Activity, and Replies. Pause to make changes, or complete the campaign. | Emails are going out on schedule, and new leads are enrolled as they arrive. |
| Paused | Edit copy, senders, schedule, and settings, then resume or complete. Sequence steps can't be added, removed, or reordered. | Sending has stopped. Lead data and statuses are preserved. |
| Completed | View Analytics, Activity, and Replies. | The campaign has ended permanently. No new leads are enrolled and no further emails go out. |

Three controls move a campaign between those states. Each one opens a confirmation modal you have to confirm — `Pause campaign`, `Resume campaign`, or `Complete campaign` — so a campaign never changes state on a single click.

| Control | What it does |
| --- | --- |
| Pause | Stops new emails going out. Leads already in progress finish their current step, and everything else waits until you resume. Pausing is also how you get back into a campaign — it's the state where copy, senders, schedule, and settings become editable again. |
| Resume | Starts sending again. New leads get sequenced, and paused leads continue from where they left off. |
| Complete | Ends the campaign permanently, and it can't be undone. Leads still in the sequence stop receiving emails and no new leads are enrolled. Analytics, Activity, and Replies all stay available afterwards. |

**Note:** Edits you make while a campaign is paused need `Save` before they take effect. `Save` sits alongside the status buttons and only lights up when there are unsaved changes, so it doubles as a quick check on whether anything is still pending.

## Pausing an individual lead

Pausing works at the lead level too, independently of the campaign around it. A paused lead in an `Active` campaign stops receiving the rest of its sequence while every other lead keeps going. The way to pause one person is through the segment feeding the campaign: take them out of it, and Clay pauses them in the campaign for you. That happens as long as `Pause lead on segment exit` is on, which it is by default.

A pause doesn't undo a lead's progress. Clay records it as a flag alongside the lead's position in the sequence, so resuming picks up at the next step rather than starting the sequence over. The pause is written to the lead's feed on the `Activity` tab as `Paused`, and you can filter the feed down to it with the `Lead status` filter.

Audience-based campaigns don't have a `Leads` tab — lead-level detail lives on `Activity`, which has a lead rail with `Search leads` for finding one person and `View all leads` for getting back to the full feed.

### Automatic pauses

Two settings under `Settings` → `Enrollment` pause leads for you:

-   `Pause lead on segment exit`: pauses a lead in this campaign when they leave the segment. It's on by default — when someone stops matching the segment feeding the campaign, the rest of the sequence doesn't go out to a lead who no longer belongs in it.
-   `Pause leads at the same company on reply`: when a lead replies, pauses other leads with the same email domain. Useful when you're sequencing several people at one account and want the conversation to happen once.

**Note:** `Pause lead on segment exit` only appears on campaigns fed by a segment. A campaign that receives its leads from a workflow has no segment to leave, so the setting isn't shown.

## FAQs

### Does relaunching a campaign charge credits again?

Credits are charged when a lead is enrolled, and a lead that's already been sequenced isn't enrolled a second time. Pausing and resuming therefore doesn't re-charge for the leads already in the campaign.

New leads arriving in the segment after you resume are charged as they enroll, at 1 action credit per lead plus any data credits your AI snippets use.

### Can I reuse a campaign after completing it?

`Completed` is a final state. A completed campaign can't be moved back to `Active` and won't enroll new leads, so reaching those people again means building a new campaign and pointing it at the segment you want.

Renaming is allowed in every state, including `Completed`, so it's worth retitling a finished campaign with something you'll recognize later once it's sitting in the list next to its replacement.
