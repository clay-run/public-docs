---
title: Sequel integration
description: Import events and attendees from Sequel, a virtual and hybrid event platform, into Clay tables.
last_synced: 2026-09-29T00:00:00.000Z
---

# Sequel integration

Import events and attendees from Sequel, a virtual and hybrid event platform, into Clay tables.

Sequel is a virtual and hybrid event platform. Use the Sequel integration in Clay to import your event catalog, find events linked to specific companies, and pull attendee lists into tables for follow-up enrichment and outreach. Sequel requires your own API key.

## Connecting Sequel in Clay

1. While in a Clay table, click `Add enrichment` and search for `Sequel`.
2. Under `Integrations`, select the Sequel action you want to use.
3. Click `+ Add account` and enter your Sequel API key to authenticate.

### `Source` Find Sequel events by company

Import a list of Sequel events associated with a specific company as rows in a Clay table.

This source is available for workspaces with Sequel sources enabled — contact Clay support to request access.

To use this source, click **Add source** and select **Find Sequel events by company**. Select the Sequel company from the dropdown (populated from your connected Sequel account) and optionally provide a start date filter. Each imported row includes a **Sequel event ID** and event metadata.

### `Source` Pull attendees from Sequel event

Import attendees from one or more Sequel events as rows in a Clay table.

This source is available for workspaces with Sequel sources enabled — contact Clay support to request access.

To use this source, click **Add source** and select **Pull attendees from Sequel event**. Enter one or more Sequel event IDs to pull attendees from. Each imported row includes the attendee's profile information and event participation details.

### `Action` Find Sequel events by ID

Look up a Sequel event by its event ID and return its details.

**Inputs**

- **Event ID (Required):** The Sequel event ID to look up.

**Output**

- **Name:** The event name.
- **Picture:** The event cover image URL.
- **Start date:** When the event starts.
- **End date:** When the event ends.
- **Timezone:** The event timezone (e.g. `America/New_York`).
- **Type:** The event type (e.g. `Virtual`).
- Additional event metadata.
