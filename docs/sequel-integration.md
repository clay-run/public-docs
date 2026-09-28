---
title: Sequel.io integration
description: Pull Sequel webinar events and attendee lists—including engagement and lead scores—into Clay tables, or look up individual events by ID.
last_synced: 2026-09-28T16:43:58.092Z
---

# Sequel.io integration

Pull webinar attendees and event details from Sequel into Clay so you can follow up based on who showed up.

Sequel is a webinar and virtual event platform for running virtual, livestreamed, and in-person events. With this integration, you can import a Sequel company's events into a table, pull the full attendee list from a finished event along with each person's engagement data, and look up any single event by its ID.

The three options differ mainly in the identifier they need, which is the easiest thing to get wrong:

| Name in Clay | Type | What it needs |
| --- | --- | --- |
| Find Sequel events by company ID | Source, which creates a new table | A Sequel company, picked from the companies on your connected account |
| Pull attendees from Sequel event | Source, which creates a new table | One or more Sequel event IDs |
| Find Sequel events by ID | Enrichment, which adds a column to a table you already have | A single Sequel event ID |

If you don't have Sequel event IDs in Clay yet, start with `Find Sequel events by company ID` — its `Id` column is the input the other two need.

## **Creating a table with Sequel**

1.  In a workbook, click `+ Add` at the bottom.
2.  Search for `Sequel` and select from the results.
3.  In the modal, you will be asked to `Select Sequel account`.
    -   If you haven't already connected your Sequel account, click `+ Add account`. You can connect either with `Sign in`, which uses your Sequel account directly, or with `API credentials`, which takes the `Client ID` and `Client Secret` found in Sequel under `Marketplace → Custom → Sequel API`. Either way, the account you connect decides which companies and events are available in Clay.

### `Source` Find Sequel events by company ID

Import every event under a Sequel company into a table, so you can pick out the ones you want attendees for.

**Inputs**

-   **Company:** The Sequel company whose events you want. Displays as a dropdown of the companies on your connected account.
-   **Start date (optional):** Only return events that start on or after this date (e.g., `2026-01-01`).
-   **End date (optional):** Only return events that start on or before this date (e.g., `2026-12-31`).
-   **Include sub-companies (optional):** Also return events belonging to sub-companies under the company you picked. On by default.
-   **Last 24 hours only (optional):** Only return events created or updated in the last 24 hours.

**Outputs**

The source creates the following columns:

-   **Id:** The event's Sequel ID, and the value `Pull attendees from Sequel event` and `Find Sequel events by ID` both run on.
-   **Name:** The event's name.
-   **Description:** The event's description, which can contain HTML.
-   **Picture:** The event's cover image.
-   **Start Date:** When the event starts.
-   **End Date:** When the event ends.
-   **Timezone:** The timezone the event is scheduled in (e.g., `America/New_York`).
-   **Registration Custom Url:** The event's registration page.
-   **Is Event Live:** Whether the event is live right now.
-   **Is Replay Enabled:** Whether a replay is available.
-   **Is Event Cancelled:** Whether the event was cancelled.
-   **Company:** The Sequel company the event belongs to.
    -   **Id:** The company's Sequel ID.
    -   **Name:** The company's name.
-   **Live Event Management:** The live and replay state of the event.
    -   **Is Event Live:** Whether the event is live right now.
    -   **Replay Enabled:** Whether a replay is available.
    -   **Event Livestream End Time:** When the livestream ended.
    -   **Replay Url:** A link to the replay recording.
-   **Recurring:** For a recurring event, how the series is set up and which iterations sit either side of this one.
    -   **Original Event Id:** The Sequel ID of the first event in the series.
    -   **Last Iteration Event Id:** The Sequel ID of the previous event in the series.
    -   **Next Iteration Event Id:** The Sequel ID of the next event in the series.
    -   **Schedule:** How often the series repeats, as a `Type` (e.g., `weekly`) and an `Every` interval.
    -   **Stopped:** Whether the series has been stopped.
    -   **Default Visibility:** The visibility new events in the series are created with (e.g., `private`).

### `Source` Pull attendees from Sequel event

Pull the attendee list for one or more finished Sequel events into a table, with each person's engagement data from the event. `Attended` marks whether each person actually showed up.

**Inputs**

-   **Event IDs:** One or more Sequel event IDs to pull attendees from. You can select these values from another table, which is how you'd chain this onto a table built with `Find Sequel events by company ID`.

**Outputs**

The source creates the following columns:

-   **Name:** The attendee's full name.
-   **Email:** The attendee's email address.
-   **Event ID:** The Sequel event this row came from, which is how you tell events apart when you pull several at once.
-   **Attended:** Whether the person attended the event.
-   **Registration Date:** When the person registered.
-   **Id:** A unique identifier for the row, combining the event ID and the attendee's email.

Sequel's scoring of the attendee:

-   **Engagement Score:** Sequel's engagement score for the attendee.
-   **Lead Score:** Sequel's lead score for the attendee.
-   **Raw Lead Score:** Sequel's raw lead score for the attendee.
-   **Lead Score Details:** The components behind the lead score.
-   **Lead Status:** The lead statuses Sequel assigned to the attendee.

How much of the event they watched:

-   **Live Time:** How long they watched the event live.
-   **Average Live View Time:** Their average live viewing session.
-   **Live Time Spent Percentage:** The share of the live event they watched.
-   **On Demand Time:** How long they watched on demand.
-   **Average On Demand View Time:** Their average on-demand viewing session.
-   **On Demand Time Spent Percentage:** The share of the recording they watched.
-   **Viewed Replay:** Whether they watched the replay.

How they took part:

-   **Questions Number:** How many questions they asked.
-   **Questions:** The questions they asked.
-   **Polls Number:** How many polls they answered.
-   **Polls:** Their poll responses.
-   **Comments:** How many chat messages they posted.
-   **Messages Reactions Count:** How many reactions they gave to messages.
-   **Circles Number:** How many circles they joined.
-   **Circles:** The circles they joined.

Timestamps:

-   **Created On:** When Sequel created the attendee record.
-   **Updated On:** When Sequel last updated the attendee record.

**Note:** Sequel refreshes its engagement data about once an hour, so the figures for an event settle up to an hour after it ends. If you pull attendees the moment an event wraps, give it an hour and run the source again to pick up the final numbers.

## **Enriching data with Sequel**

1.  While in a Clay table, click `Add enrichment` and search for `Sequel`.
2.  Under `Integrations`, select `Find Sequel events by ID`.
3.  In the modal, you will be asked to `Select Sequel account`.

### `Action` Find Sequel events by ID

Look up a single Sequel event by its ID and return its details.

**Inputs**

Required:

-   **Event ID:** The ID of the Sequel event to look up.

**Outputs**

-   **Name:** The event's name.
-   **Type:** How the event runs — `Virtual`, `LiveStream`, or `InPerson`.
-   **Picture:** The event's cover image.
-   **Start Date:** When the event starts.
-   **End Date:** When the event ends.
-   **Timezone:** The timezone the event is scheduled in (e.g., `America/New_York`).
-   **Presenters:** The event's presenters.
-   **Organizers:** The email addresses of the event's organizers.
-   **Event Info:** Further details Sequel holds on the event.
-   **Registration:** The event's registration settings.
-   **Is Registration Mode Enabled:** Whether registration is turned on for the event.
-   **Is Attendee Registration Mode Enabled:** Whether attendees have to register.
-   **Is Presenter Registration Mode Enabled:** Whether presenters have to register.
-   **Disable Event Recording:** Whether recording is turned off for the event.
-   **Close Captioning Settings:** The event's closed captioning settings.
-   **Sequel AI:** The event's Sequel AI settings.

### **Run settings**

-   **Auto-update:** Useful when event IDs keep landing in the table, so each new row is looked up as it arrives rather than waiting for you to re-run the column.
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

## **FAQs**

### Can I pull attendees from several events in one table?

Yes — `Event IDs` takes as many as you want to give it. The source works through the events one at a time and 100 attendees at a time, filling rows in as it goes, so a large multi-event pull keeps running for a while after the first rows land.

### Why is one of my event IDs coming back empty?

The two actions handle an ID that Sequel can't find differently, which is worth knowing when you're troubleshooting a column.

-   `Find Sequel events by ID` leaves the cell blank and the column finishes, so unmatched rows are simply empty.
-   `Pull attendees from Sequel event` stops the run and names the ID it couldn't find, so a single bad ID will hold up the whole import.

### Can I create or update events in Sequel from Clay?

Not from this integration — it reads from Sequel rather than writing back, so build and edit events in Sequel and use Clay for what happens after them. A common pattern is to pull attendees into a table, enrich them, and send the ones worth a follow-up to your sequencer or CRM.

### Why does the `Company` dropdown only show one company?

`API credentials` connections are scoped to the single company those credentials belong to, so that company is the only option you'll see. If you need events from several companies, reconnect with `Sign in` instead — that method pulls the full list of companies your Sequel account can reach.
