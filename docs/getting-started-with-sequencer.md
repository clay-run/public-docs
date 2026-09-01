---
title: Getting started with Sequencer
description: An overview of Sequencer, Clay's cold email tool, covering infrastructure setup, campaign building, deliverability best practices, and plan limits.
last_synced: 2026-09-01T04:56:15.508Z
---

# Getting started with Sequencer

Sequencer runs cold email campaigns at scale from your Audiences data, handling sending infrastructure, copy, and deliverability in one place.

Sequencer runs cold email campaigns at scale from your Audiences data, handling sending infrastructure, copy, and deliverability in one place.

Sequencer is Clay's cold email tool: you point a campaign at a set of leads, write a sequence of up to four emails, and Clay paces the sending across your email accounts. You'll find it under `Campaigns` in the sidebar, where each campaign is one sequence sent to one set of leads.

There are two ways to build one, and the difference is where the leads come from:

-   A segment-based campaign — labeled `People` on the `Campaigns` page — draws from a segment of People in Audiences and enrolls leads continuously as they enter it.
-   A table-based campaign — labeled `Table` — syncs rows from a Clay table in a workbook. Segment-based is the better starting point for anything new, and [Table-based campaigns](https://university.clay.com/docs/email-sequencer) covers the other path.

This page is the map. Each section below covers one stage of getting a campaign out the door, and links to the doc that walks through it.

## What Sequencer is (and isn't)

Sequencer is built for sending cold email at volume — to people who don't yet know your brand — and it's aimed at Marketing Ops and Sales Ops rather than individual reps. A sequence holds up to four emails, and in almost every campaign the first one does most of the work; the follow-ups mainly nudge the thread back up the inbox.

It's designed around the three things that decide whether cold outbound works: reaching the right people, writing copy worth replying to, and landing in the primary inbox instead of Spam.

It's worth being clear about what Sequencer isn't, because the word "sequencer" covers several different kinds of product:

-   **Not a sales engagement platform.** There's no dialer, and no way to assign tasks to reps. Everything Sequencer does is automated sending at scale rather than manual steps fanned out to a team, so it won't replace the tools reps work out of all day.
-   **Not lifecycle or marketing email.** You send from dedicated sending accounts rather than any address on your domain, and the volume limits are much lower than a marketing email platform's.
-   **Not speed-to-lead.** Sending is paced deliberately over hours or days to protect deliverability, so it isn't the right tool for replying to a form fill within minutes.

For how cold and warm leads differ, and how the two ways of building a campaign compare, see [Sequencer FAQs and best practices](https://university.clay.com/docs/sequencer-faqs-and-best-practices).

## Set up your sending infrastructure

Before anything can send, you need email accounts. There are two ways to get them, and the choice matters more than it looks.

**Buy them in Clay.** This is the recommended path, and buying email accounts is available on Growth and Enterprise plans. Clay sets up brand-adjacent domains and official Google Workspace or Microsoft Outlook accounts, gets the DNS records right, and manages warmup for you. Because Clay controls these accounts, it can also debug them end to end if something goes wrong.

**Bring your own.** Use this when you're on Launch, when you want to send from your real main domain, or when you're migrating accounts you already bought elsewhere. It takes more setup — including a one-time authorization by your Google Workspace or Microsoft administrator — and the ongoing account health is yours to monitor.

Either way, warmup is what makes a new account safe to send from. See [Buying email accounts in Clay](https://university.clay.com/docs/buying-email-accounts), [Connect your own email accounts](https://university.clay.com/docs/connect-your-own-email-accounts), and [Email warmup](https://university.clay.com/docs/email-warmup).

## Get your leads ready

Sequencer doesn't build or enrich lead lists — it sends to lists you've already built. The prerequisite people most often miss is that a segment-based campaign draws only from Audiences, so leads have to be there before it can touch them.

At a minimum, that means a segment of People in Audiences and an email address on each of those people. Qualification, research, and email-finding all happen upstream, in search, workflows, and Audiences.

This is also the right moment to set up exclusions, so your first send skips existing customers and anyone on your do-not-contact list. See [Get leads ready to sequence](https://university.clay.com/docs/get-leads-ready-to-sequence).

## Build and launch your campaign

A campaign has four parts, and while it's still a draft you can move between them in any order:

-   **Leads** — the segment it draws from
-   **Sequence** — the emails it sends
-   **Sender accounts** — the inboxes it sends from
-   **Settings** — schedule, tracking, and enrollment behaviour

Sequences default to plaintext, because HTML tends to hurt deliverability on cold sends. You personalize copy with variables drawn from your lead data, AI snippets that write from that data, and spintax to vary wording between sends. You can also run two copy variants against each other and keep whichever performs better.

Launching starts the sending and locks the shape of the sequence — once a campaign is live you can't add, remove, or reorder steps. Pausing it reopens everything else: copy, the wait between steps, and the campaign's settings are all editable again.

See [Build your sequence](https://university.clay.com/docs/build-your-sequence), [A/B test your sequence copy](https://university.clay.com/docs/ab-test-sequence-copy), and [Launch and manage a campaign](https://university.clay.com/docs/launch-and-manage-a-campaign).

## Watch the results

Once emails are going out, campaign analytics show the lead funnel: how many people were sent to, how many replied, and how those replies were categorized. Clay tags every reply by sentiment, so genuine interest is easy to separate from out-of-office auto-replies.

The metric worth optimizing is the positive reply rate rather than the raw reply rate. A campaign can look busy while generating nothing useful.

Every campaign activity also lands in an events table, which is an ordinary Clay table — so you can automate on top of it, from CRM sync to AI-drafted replies routed for approval. See [Campaign analytics and replies](https://university.clay.com/docs/campaign-analytics-and-replies) and [Automate campaign events](https://university.clay.com/docs/automate-campaign-events).

## Keep your deliverability healthy

Deliverability is the quiet thing that decides whether a campaign works at all: whether your email reaches the primary inbox rather than Spam or Promotions. Most of Sequencer's defaults exist to protect it.

Send roughly 20 emails per day per inbox, keep each domain to 3 inboxes and 5 at the most, and give new accounts around three weeks of warmup before pushing volume through them. Open and click tracking are off by default, and we'd suggest leaving them that way — they hurt cold deliverability, and now that providers prefetch images they no longer measure much.

**Note:** A bounce rate at or above 5% is the point to stop and look at your lead list and sender accounts. High bounce rates carry over into your sender reputation, which is much slower to repair than it is to protect.

For domain strategy, monitoring, and what to do when a domain's reputation slips, see [Deliverability and domain health](https://university.clay.com/docs/sequencer-deliverability).

## Costs, plans, and limits

Segment-based campaigns are available on Launch, Growth, and Enterprise plans; buying email accounts in Clay needs Growth or Enterprise. Each lead enrolled in a campaign costs 1 action credit, plus variable data credits for any AI snippets in your copy — the campaign editor shows an estimate before you launch.

Credit budgets are set up at the workspace level, and you attach one to a campaign when you launch it. Once a budget's limit is reached, the campaigns drawing on it stop spending credits, which stops new leads enrolling.

The hard limits, in one place:

| Limit | Value |
| --- | --- |
| Emails per sequence | 4 |
| Maximum delay between steps | 10 days |
| Leads per campaign | Up to 500,000 |
| Message size | 8 KB of text per email |
| Copy variants per campaign | 2 |
| Sequences per lead, per campaign | 1 |
| Send limit per email account, per day | 10–500 (30 for accounts bought in Clay) |

Credit costs, plan differences, and what happens to existing table-based campaigns are covered in [Sequencer FAQs and best practices](https://university.clay.com/docs/sequencer-faqs-and-best-practices).
