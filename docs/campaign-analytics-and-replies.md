---
title: Campaign analytics and replies
description: How to read campaign analytics, interpret reply sentiment categories, answer replies from within Clay, and manage the workspace blocklist.
last_synced: 2026-09-01T03:15:06.240Z
---

# Campaign analytics and replies

Where to read the results of a live campaign — the lead funnel, reply sentiment, and the per-lead activity feed — plus how to answer replies and keep a blocklist.

A live campaign gives you three tabs for reading what came back. `Analytics` has the numbers, `Activity` has the event-by-event detail for every lead, and `Replies` is where you answer people. The `Campaigns` page adds workspace-wide versions of the first and the last of those, through the `Analytics` and `Inbox` buttons in its header, so you can also read across every campaign at once.

## Campaign analytics

Open a campaign and select `Analytics`. The date filter in the top right sets the window for the page:

-   `Today`
-   `Last 7 days`
-   `Last 30 days`
-   `This week`
-   `This month`
-   `Last month`
-   `Custom range`
-   `All time` — the default

If the campaign is running an A/B test, a sequence filter lets you narrow to one variant, or set two of them side by side.

### Lead funnel

Four cards open the page. They always report the current state of every lead, whatever the date filter says.

| Card | What it counts |
| --- | --- |
| Processed | Leads that have entered the campaign, including queued and failed enrollments. |
| Enrolled | Leads that enrolled successfully and can receive emails. |
| Complete | Enrolled leads that reached a terminal state — replied, finished the sequence, bounced, or unsubscribed. |
| Paused | Leads that are paused right now. The card appears only when there are some. |

### The rest of the page

The remaining sections run down the page in this order.

| Section | What it reports |
| --- | --- |
| Lead status snapshot | Splits leads into In progress and Complete, then breaks them out further into Queued, one bar per step a lead is sitting on, Replied, Completed, Bounced, Unsubscribed, and Invalid enrollment. Paused leads stay in whichever bucket they belong to and show up as a hatched portion of it. |
| Sequence conversion | Reads across the sequence rather than across leads. For each step, how many enrolled leads received it and what happened there — Replied, Bounced, No reply yet, and Queued for sends still to come. |
| Replies | Reply volume and category, which the next two sections of this doc go into. |
| Campaign statistics | Totals Sent, Replies, Bounces, and Unsubscribes over the selected date range, adding Opens and Clicks when you have that tracking turned on, with a daily chart underneath. |
| Deliverability | Delivery and bounce rates broken down by provider, account, and domain. |

[Deliverability and domain health](https://university.clay.com/docs/sequencer-deliverability) covers how to read the `Deliverability` section and what to do about what you find.

**Note:** `Lead funnel` is the one section that ignores the date filter, because it answers where your leads stand right now. Everything below it is scoped to the window you picked, so the two line up most cleanly on `All time`.

## Workspace-wide analytics

To compare performance across every campaign, select `Analytics` in the header of the `Campaigns` page. A `Campaigns` filter and a date range at the top scope the whole page.

Five cards lead the page, each pairing a rate with the count behind it: `Emails sent`, `Reply rate`, `Bounce rate`, `Sender bounce rate`, and `Open rate`.

| Section | What it reports |
| --- | --- |
| Engagement | Positive replies, Negative replies, and Neutral replies, each as a rate with the reply count beside it. The section worth the most attention. |
| Leads | People rather than emails. Total unique leads covers launched and completed campaigns, First touch is leads that have had only the first email in a sequence, and Follow-up is leads that have had at least one email after that. |
| Email reach | Sending volume over time. |
| Sender bounces | Bounces by domain and by individual account. Deliverability work — the deliverability doc linked above covers that table. |

## Reply sentiment tagging

Every reply gets a category automatically, and each category carries a sentiment. That sentiment is what rolls up into the positive, negative, and neutral figures in analytics, so the categories are worth a read.

| Sentiment | Category | What it usually means |
| --- | --- | --- |
| Positive | Interested | The lead wants to keep talking. |
| Positive | Meeting request | The lead is asking for a call or a demo. The strongest signal in the set. |
| Positive | Info request | The lead is asking for pricing, detail, or material before committing. |
| Neutral | Out of office | An automatic away reply rather than a person. |
| Neutral | Wrong person | The lead isn't the right contact, and often names who is. |
| Neutral | Uncategorized | The reply didn't fit any other category clearly. Worth reading by hand. |
| Negative | Not interested | A decline, without a request to stop contacting them. |
| Negative | Do not contact | An explicit request to stop. Add these to your blocklist. |
| Negative | Sender-originated bounce | A rejection generated by the sending side rather than a reply from the lead. |

Categorization is a starting point rather than the last word. Open a reply, use `Change lead category` from its 3-dot menu, and the correction flows through into that campaign's analytics.

**Note:** `Out of office` sits in the neutral group, so a run of auto-replies never inflates your positive numbers. They are still worth something as a signal: an away reply means the email reached a real, monitored mailbox.

## The metric that matters

Raw reply rate counts every reply, which means it moves the same amount when someone asks for a meeting and when someone tells you to stop emailing. Positive reply rate counts only the replies you want more of. That is the number to optimize a campaign against, and the number to compare two campaigns on.

### Where to find it

`Positive replies` under `Engagement` in the workspace-wide `Analytics` gives you the whole workspace, and the `Positive` card in the `Replies` section of a campaign's `Analytics` gives you one campaign. Filtering a campaign's analytics to a single A/B sequence adds a reply-rate line with the absolute counts spelled out — replies out of leads delivered to, and how many of those were positive.

### Two denominators

Reply rate uses two different denominators depending on where you read it, which is worth knowing before you compare the two:

-   Campaign-wide `Reply rate` divides replies by emails sent.
-   A single sequence's reply rate divides replies by leads delivered to, which is sends minus bounces.

The same campaign therefore reads lower campaign-wide, and Clay notes as much in a tooltip on the sequence figure. Neither number is wrong — they answer slightly different questions, and the per-sequence one is the fairer basis for comparing two pieces of copy.

### What can skew the number

The `Reply rate` card counts out-of-office auto-replies along with everything else. Hover it for the same figure excluding out of office, and the `Out of office` card beside it shows how many there were.

Give a cohort time before you draw a conclusion from it. Replies lag sends by days, so a campaign that started this week reads low for reasons that have nothing to do with the copy. Clay treats a send as old enough to have plausibly drawn a reply after three days, and the per-sequence view reports sample size and maturity alongside the rate for exactly that reason.

## The Activity feed

`Activity` is the per-lead, per-email event stream: every send, open, click, reply, bounce, and unsubscribe, newest first and grouped by day. Campaigns built from an audience don't have a separate leads tab, so this is where lead-level detail lives.

A rail on the left lists the campaign's enrolled leads with a `Search leads` box. The feed opens on `All leads` — select someone to narrow it to their events, and `View all leads` brings you back.

### Filtering the feed

Two filters sit above the feed.

| Filter | Narrows to |
| --- | --- |
| Email type | Sent, Opened, Clicked, Replied, Bounced, or Unsubscribed. |
| Lead status | Enrollment outcomes such as Enrolled, Enrollment failed, Paused, and Stopped, plus the reply categories above. |

### Where the events go

Every activity also writes back onto the person's record in Audiences, with company-level rollups alongside it. That means anything you see in this feed is also available for segment building, workflows, and reporting outside the campaign — see [Audiences](https://university.clay.com/docs/audiences).

A campaign writes its events to a Clay table as well, which is where automations get built on top of them. The `Events` button on the `Campaigns` page opens that table, covering the campaigns built from a segment; for a table-based campaign, open the table linked to the campaign instead. [Automate campaign events](https://university.clay.com/docs/automate-campaign-events) covers the table itself, the actions available on it, and the automations worth setting up.

## Replying to leads

Replies come back into Clay, so you can answer without leaving the app. They go out from the exact account the original email was sent from, which keeps the thread intact on the recipient's side.

### The campaign Replies tab

The campaign `Replies` tab lists that campaign's conversations. Each row shows the lead, the campaign name, a category badge, and a dot while the thread is unread.

Select one to read the whole exchange, then use `Reply` or `Forward`. The same 3-dot menu holds `Change lead category` and a single read-state item that flips with the thread: it reads `Mark as read` while the thread is unread, and `Mark as unread` once you've read it.

### The workspace inbox

For everything at once, select `Inbox` in the header of the `Campaigns` page. It's the same reading and replying experience, with a campaign list down the side and a `Search` box for finding one.

A person filter narrows the inbox to the leads assigned to a single teammate, and defaults to `All (workspace)`.

### Who can reply

Replying and forwarding are available to workspace editors and admins. Reps invited under the `Sales Rep` role get their own inbox view, scoped to the leads assigned to them — a good fit when a campaign hands conversations off to a sales team.

**Note:** Clay can only fetch replies while a sender account is reachable. When it can't — usually an auth error or a provider rate limit — that account stops sending too, and the replies waiting on it come through once the connection is restored. An auth error is the one to act on: reconnect the account under `Email accounts`, rather than pausing leads by hand.

## Managing your blocklist

The blocklist is the set of email addresses and domains Clay will never contact from a campaign, and it applies across the whole workspace. It's the fastest way to honor a do-not-contact request, and it's also one of the first things to check when a lead never received anything.

Open the `Blocklist` tab on the `Campaigns` page to see it. Each row shows:

-   `Type` — either `Email` or `Domain`
-   `Email or domain` — the address or domain itself
-   `Date added`

`Search blocklist` and the `Type` filter narrow a long list.

### Adding entries

Select `Add to blocklist`. The modal has two tabs:

-   `Manual` — a single `Email or domain`.
-   `Import CSV` — a file with one address or domain per line, up to 1,000 entries at a time.

You can also block someone mid-conversation:

-   From a reply's 3-dot menu, `Add lead to blocklist` blocks that one address.
-   From the same menu, `Add domain to blocklist` blocks everyone at their company.
-   The `Add email to blocklist` action on the campaign events table does the same thing as part of an automation.

### Removing an entry

Open its 3-dot menu in the blocklist, select `Delete`, and confirm with `Remove from blocklist`.
