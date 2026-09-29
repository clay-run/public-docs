---
title: Sequel integration
description: Use Sequel in Clay to pull attendee engagement data from webinars into Clay tables for post-event outreach personalization.
last_synced: 2026-09-29T00:00:00.000Z
---

# Sequel integration

Use Sequel in Clay to pull attendee engagement data from webinars into Clay tables for post-event outreach personalization.

Sequel is a webinar and virtual event platform. With this integration you can look up event metadata by ID and pull attendee engagement data into a Clay table for post-event outreach personalization. Source actions that populate a table from a full event list are currently in beta.

## Using Sequel in Clay

1.  While in a Clay table, click `Add enrichment` and search for `Sequel`.
2.  Under `Integrations`, select one of the Sequel actions.
3.  In the modal, click `+ Add account` and connect your Sequel account via OAuth.

### `Action` Find Sequel events by ID

Given a Sequel event ID, return that event's metadata: name, start/end dates, timezone, type (Virtual, LiveStream, or InPerson), presenters, organizers, and registration settings.

**Inputs**

-   **Event ID (Required):** The ID of the Sequel event to look up.

### `Source` Find Sequel events by company

Given a Sequel company, return the list of all events under that company — with event IDs, names, dates, type, and status. Use this to discover which events exist before pulling attendees.

**Currently in beta — contact support to enable.**

**Inputs**

-   **Company (Required):** Select the Sequel company from the dropdown.
-   **Start date / End date (Optional):** Filter events by start date range.
-   **Include sub-companies (Optional):** Include events from sub-companies (default: enabled).
-   **Last 24 hours only (Optional):** Return only events created or updated in the last 24 hours.

### `Source` Pull attendees from Sequel event

Pull the full list of attendees from a completed Sequel event into a Clay table, including engagement data — live minutes watched, on-demand minutes, poll responses, Q&A, and chat activity. Best used for post-event outbound personalization.

**Currently in beta — contact support to enable.**

**Note:** Sequel's analytics engine runs hourly. Engagement data may have up to approximately 1 hour of latency after an event ends.

**Inputs**

-   **Event ID (Required):** The Sequel event ID to pull attendees from.
