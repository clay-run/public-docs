---
title: Scheduled tasks
description: Set recurring tasks for Clay's global agent to run daily, on weekdays, weekly, or monthly, and manage, pause, or end those schedules.
last_synced: 2026-10-08T15:37:07.895Z
---

# Scheduled tasks

Set a task to run on its own — daily, on weekdays, weekly, or monthly — so recurring go-to-market work happens without you starting it.

A scheduled task is a piece of recurring work you hand to Clay's global agent. Clay starts each run on the cadence you set, and pauses a run that needs your input.

Scheduled tasks live under `Scheduled` in the sidebar of `Agent`, the left-nav tab where you tell Clay what to work on. For what a task can reach and what it costs, see [Clay's global agent](https://university.clay.com/docs/global-agent).

**Note:** Write the instructions to stand on their own — name the segment, workflow, or campaign rather than pointing back to the one from last time.

## Scheduling a task

1.  In the `Agent` sidebar, open `Scheduled`, then select `Schedule`.
2.  On the `What should run on its own?` screen, start from a template or describe the task and cadence in your own words. The templates are `Weekly pipeline priorities`, `Weekly account coverage review`, and `Monthly workflow optimization review`.
3.  Clay proposes the schedule and you edit it before confirming:
    -   `Instructions` — what Clay follows each run. Say what to do and when to stop; the cadence comes from the fields below.
    -   `Frequency` — `Daily`, `Weekdays`, `Weekly`, or `Monthly`.
    -   `Time` — the run time on your own clock — plus `Day` on a weekly schedule.
    -   `Starts`, and `End date` if it should stop on a set date.

You can also ask for a schedule inside a task — say what should run and how often, and Clay fills in the same cadence fields for you to check and confirm. Ask for a cadence the fields don't offer, such as every other week, and Clay builds that too. **Note: a schedule runs at most once a day.**

## Managing a schedule

The same controls follow a schedule from the `Scheduled` list to its own page.

| Control | What it does |
| --- | --- |
| Run now | Runs it once, outside its cadence. Available once the current run finishes. |
| Pause / Resume | Stops future runs. Resuming rejoins the cadence at its next slot, so runs missed while paused don’t happen later. |
| Mark as complete | Ends the schedule and keeps its runs on record. It starts running again only if you give it a cadence with a future date. |
| Delete | Removes the schedule, its runs, and the tasks those runs created. This can’t be undone, and it’s unavailable while a run is in progress. |

Once it's saved, the `Scheduled` list shows each schedule's `Next run`.  
A schedule's own page holds the `Instructions` it runs, which you can edit, and every run it has had.

A schedule also carries its own permission level, set from that page rather than from the message box. That lets a run nobody is watching be held tighter than a task you start yourself — see [Clay's global agent](https://university.clay.com/docs/global-agent#permissions-and-approvals) for what each level allows.

## FAQs

### Who does a scheduled run act as?

It runs as the person who created the schedule, so it reaches what that person can reach in Clay. `Scheduled` lists the schedules you created.

A schedule runs only while its creator can still edit in the workspace. If they leave, it stops and is marked complete.

### What happens when a run stops for input?

The schedule's row on `Scheduled` reads `Waiting on you`, and the waiting run carries a `Needs input` pill on the schedule's own page. Opening that run takes you to the task it created, where you can answer and let it carry on.

While a run is waiting, the schedule stands still: the next run on its cadence is skipped rather than queued, and `Run now` stays unavailable until the waiting run finishes.

With several schedules going, filter the `Scheduled` list by `Needs input` to see just the ones waiting on you.

### Will it stop on its own?

On a date, yes — turn on `End date` and set `Ends`, and the schedule finishes after its last run.

A target in `Instructions` works differently. "Book meetings for the AE and stop once 25 are booked" shapes each run rather than ending the schedule: where Clay can read that number from your workspace data, it takes the reading first, skips work already done, and says where the total stands in its reply.

To end a schedule yourself, use `Mark as complete` or `Delete`.
