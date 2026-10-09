---
title: Automate campaign events
description: Build automations in the Campaign events table to act on sends, replies, bounces, and unsubscribes from your segment-based campaigns.
last_synced: 2026-09-01T03:12:18.496Z
---

# Automate campaign events

Learn how to build automations on the Campaign events table, where every send, reply, bounce, and unsubscribe from your campaigns lands as a row in Clay.

Every campaign writes its activity into a Clay table called `Campaign events`, with one row per event. Because it's an ordinary Clay table, anything you'd normally do in Clay — formulas, AI columns, integrations, actions — you can do in response to something a lead did.

## The campaign Events table

A single table covers every segment-based campaign in your workspace, so you can set an automation up once instead of rebuilding it per campaign.

### Opening the table

To open it:

1.  Go to `Campaigns` from your home screen.
2.  Click `Events` in the page header, next to `Inbox` and `Analytics`.

Clicking `Events` creates the table if it doesn't exist yet, and opens it if it does. You don't need a live campaign to get started — build your automations while the campaign is still a draft, and rows will begin arriving once emails go out.

`Events` covers segment-based campaigns. If you're looking for activity from an older table-based campaign, open the table linked to that campaign instead — those campaigns write their events into a table in the same workbook.

### Event types

Each row records one thing that happened to one lead. The `Event type` column tells you which:

| Event type | Name when you configure a webhook | What it records |
| --- | --- | --- |
| EMAIL_SENT | Email sent | An email in the sequence went out to the lead. |
| EMAIL_REPLY | Email reply received | The lead replied to one of your emails. |
| EMAIL_OPEN | Email opened | A tracked open was recorded. |
| EMAIL_LINK_CLICK | Email link clicked | A tracked link click was recorded. |
| EMAIL_BOUNCE | Email bounced | The message couldn't be delivered. |
| LEAD_UNSUBSCRIBED | Lead unsubscribed | The lead opted out of further email. |
| LEAD_CATEGORY_UPDATED | Lead category updated | The category on a lead's reply changed. |
| CAMPAIGN_STATUS_CHANGED | Campaign status changed | The campaign moved between states, such as going live or being paused. |

**Note:** Events are targeted to land in the table within five minutes for 99% of events. That target covers sender accounts bought through Clay, since those are the accounts Clay manages end to end.

### Lead and campaign context

The remaining columns give you the context to act on:

-   `Campaign ID`: which campaign the event came from.
-   `Lead ID` and `Audience ID`: identifiers for the lead, useful for matching rows to records elsewhere.
-   `Lead email address`: the address the email was sent to.
-   `Sender email address`: the sending account involved in the event.
-   `Last reply content`: the body of the lead's reply, on reply events.
-   `Reply category`: the category assigned to a reply, so you can separate positive replies from the rest.
-   `Audience record`: looks up the lead's record in Audiences, which brings every field you've enriched there into reach.

The default view is filtered to the event types most people act on. Edit or clear that filter to see everything the table is receiving.

### Campaign activity in Audiences

Campaign activity is also written back onto each lead's record in Audiences, with rollups at the company level. If all you want is to segment on who replied or who bounced, you can do that in Audiences without touching this table.

## Common automations

A few patterns come up again and again. Each one starts the same way: filter the table to the event type you care about, then add the columns that do the work.

-   **Draft and send replies for you.** Filter to reply events, add an AI column that reads `Last reply content` and drafts a response, then run the reply action on the result. When the reply is predictable, a saved template or a booking link works just as well as generated copy.
-   **Put a person in the loop first.** Rather than sending the draft straight out, post it to a Slack channel for approval using Clay's Slack actions, and only run the reply action once someone signs off. This is the usual middle ground for teams that want the speed without an unreviewed send.
-   **Hand the reply to whoever owns the relationship.** `Get rep email` resolves the rep behind the sending account, and `Forward email` passes the thread on to them. Both columns are pre-built in the table.
-   **Keep your blocklist current.** Run `Add email to blocklist` on unsubscribe events so those addresses are skipped by future campaigns.

## Syncing to your CRM

Your CRM integration works here exactly as it does in any other Clay table. The advantage of syncing from events rather than from a campaign is precision: you choose which rows are worth a CRM record instead of pushing everything.

A common setup:

1.  Filter the table to reply events with a positive `Reply category`.
2.  Create or update a record for just those leads.
3.  Use `Only run if` on the export column to keep it firing on the rows you intended.

`Audience record` gives the export column access to the enriched fields on the lead, so the record you write can carry more than an email address. For a breakdown of which categories count as positive, see [Campaign analytics and replies](https://university.clay.com/docs/campaign-analytics-and-replies).

## Available actions

Four action columns come pre-built in the table:

| Action column | What it does |
| --- | --- |
| Reply to lead email | Sends a reply back into the existing thread, from the account that sent the original email. Draft the response in Email reply: Body first — the draft column inside the Email reply field group. Carries a condition: it runs only on a reply event, only when there's a draft in Email reply: Body, and never on a reply category where a response isn't wanted. |
| Add email to blocklist | Adds the lead's address to your blocklist so future campaigns skip them. |
| Get rep email | Looks up the rep who owns the sending account behind the event. |
| Forward email | Forwards the lead's reply to another address, such as the one returned by Get rep email. |

These arrive as run-on-click columns, so nothing fires until you run it — row by row, or across a filtered selection. Their run settings work like any other action column in Clay, so you can move from clicking to running on a condition once you trust the output.

The names above are the column names Clay provisions in the table. If you're adding one of these actions yourself, search the action picker for its action name instead — several read differently there:

-   `Reply to lead email` is `Reply to lead in campaign`
-   `Add email to blocklist` is `Add email or domain to blocklist`
-   `Get rep email` is `Get rep data`
-   `Forward email` is `Forward lead email in campaign`

### Adding other actions

You can add any other Clay action to the table as well — the same catalog you'd reach in any Clay table, so an event can trigger a Slack message, a CRM write, or an enrichment.

`Pause lead in campaign` is one of them, and it's the direct way to stop a lead's sequence in response to something outside the campaign — they registered for an event, say, or filled in a form. Search for it by name when you add the action column.

Removing the lead from the segment the campaign is attached to has the same effect: with `Pause lead on segment exit` enabled, leaving the segment pauses them automatically.

## Custom webhooks

You only need a webhook if you want campaign events somewhere other than the `Campaign events` table, such as an internal service or a tool that routes outbound activity into your own stack.

Add one from the campaign's `Settings` tab, under `Webhooks`:

1.  Click `Add webhook`.
2.  Enter a `Webhook name`.
3.  Paste the destination into `Webhook URL`.
4.  Choose which `Event types` to send.
5.  Click `Add webhook` at the bottom of the form.
6.  Click `Save` to persist it on the campaign.

An event type can belong to only one of a campaign's webhooks. Once you've assigned it, it shows as unavailable in the `Event types` picker of every other webhook on that campaign.

Webhook settings follow the same rules as the rest of a campaign's settings — set them before you launch, or pause the campaign to change them.

## FAQs

### Some events haven't shown up. What should I check?

The usual cause is the inbox behind the campaign being processed slowly, or being temporarily unreachable because of an auth error or a provider rate limit.

An auth error is the one to act on: reconnect the account under `Email accounts`. A rate limit or a backed-up mailbox clears on its own, and the waiting events land once the connection recovers. Pausing leads by hand doesn't help either way. If events are still missing once the account is reachable again, contact support.

### Will the reply action send to someone who told me no?

No. `Reply to lead email` skips the reply categories where a response isn't appropriate: `Out Of Office`, `Wrong Person`, `Not Interested`, and `Do Not Contact`.

Anything you build yourself is up to you, so it's worth adding the same guard to your own reply columns. [Campaign analytics and replies](https://university.clay.com/docs/campaign-analytics-and-replies) covers the full set of categories.

### Do I need tracking enabled to get open and click events?

Open and click events only appear when you've turned on `Track email opens` and `Track link clicks` in the campaign's settings, and click tracking needs HTML enabled.

Neither is recommended for cold outbound, because tracking works against deliverability and prefetching by providers like Apple Mail makes the numbers unreliable. Replies are the signal worth building on — [Deliverability and domain health](https://university.clay.com/docs/sequencer-deliverability) has the reasoning in full.
