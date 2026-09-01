---
title: Deliverability and domain health
description: How to protect your sending reputation so campaign emails land in the inbox, covering volume guidelines, domain health monitoring, and when to rotate to fresh domains.
last_synced: 2026-09-01T03:09:37.527Z
---

# Deliverability and domain health

How to protect your sending reputation so campaign emails land in the inbox, covering volume guidelines, the health numbers to watch, and when to move to fresh domains.

Deliverability is the difference between an email that arrives in someone's primary inbox and one that never gets read. Clay handles the technical setup for the sending accounts you buy through it, which leaves you the parts that matter most day to day: how much you send, who you send it to, and how you read the signals coming back.

## What deliverability means

Deliverability is about landing in the primary inbox rather than Spam or Promotions. Two questions sit behind it: whether a mailbox provider accepts the email at all, and where it files the email once accepted. A rejected email shows up as a bounce, and an accepted one can still be filtered.

Providers answer both questions using the reputation of the domain and the mailbox you send from. Reputation is built from history — how much you send, how steadily you send it, and how recipients respond. Replies and other positive engagement build reputation up. Bounces, spam complaints, and sudden jumps in volume pull it down.

**Note:** The `Spam check` grade in the sequence editor is a lightweight heuristic that catches common flags in your copy. It is a useful last look before you launch, not a prediction of where your email will land.

Two related topics live in their own docs. Compliance for the EEA and the UK is covered in [Best practices for B2B email direct marketing](https://university.clay.com/docs/direct-marketing-best-practices), and [Za-zu's Cold Email Handbook](https://za-zu.com/docs/handbook/intro) is a thorough deep dive on the craft of cold email itself.

## Why cold outbound needs alternate domains

Cold campaigns reach people who don't know your brand yet, so a share of recipients will ignore the email or mark it as spam. That response is normal for cold outbound, and it attaches to the domain the email was sent from. Sending cold volume from a brand-adjacent domain keeps that history off the domain your business depends on for customer replies, invoices, and recruiting.

### Buying accounts from Clay

Buying accounts from Clay is the path built for this. Clay provisions managed domains alongside official Google Workspace and Microsoft Outlook accounts, keeps SPF, DMARC, and DKIM correct, and runs warmup for you. You choose brand-adjacent domains during the purchase wizard — something close to your real domain, so the sender still looks like your company.

For the full purchase flow, see [Buying email accounts in Clay](https://university.clay.com/docs/buying-email-accounts).

### Bringing your own accounts

Bringing your own accounts makes sense when you want to send from your real main domain, usually to warmer leads at lower volume. One thing is worth knowing before you choose: Clay can monitor domain deliverability for the accounts it manages, and that monitoring isn't available for accounts you bring yourself.

For the full connection flow, see [Connect your own email accounts](https://university.clay.com/docs/connect-your-own-email-accounts).

## Volume guidelines

Steady, human-looking volume is the single biggest lever you control. The numbers below are the starting points we recommend for cold campaigns.

| Guideline | Where to start | What it does for you |
| --- | --- | --- |
| Emails per inbox per day | About 20 | Keeps each mailbox in the range a provider expects from a person rather than a bulk sender. |
| Inboxes per domain | 3, up to a maximum of 5 | Spreads a campaign's volume across several mailboxes so no single one carries all of it. Each domain you buy from Clay includes 3 sender accounts, and 5 is the most a domain will hold. |
| Warmup before high volume | About 3 weeks | Gives a new inbox a history of ordinary sending and receiving before campaign traffic starts. |
| Per-account daily send limit | About 20, the default for accounts you link yourself | Leaves headroom on purpose. Accounts you link yourself accept 10 to 500, and accounts bought from Clay can go up to 30 a day. |

To send more per day, add more sender accounts to the campaign before you raise per-account limits. More accounts means the same volume spread thinner, which is exactly what you want. You can adjust a limit from the 3-dot menu on any account under `Email accounts`, using `Update send limit`.

The campaign schedule shapes pacing too. Choosing `Optimized for deliverability` as the `Schedule type` sends Monday to Friday between 09:00 and 17:00, with a `Min time between emails (min)` of 20 — business hours, evenly spaced, the way a person sends.

## Monitoring domain health

Clay gives you a workspace-wide view and a per-campaign view, and they answer different questions.

### Across the workspace

For the state of your whole sending setup, open `Analytics` from the `Campaigns` page.

-   Top-line cards: `Emails sent`, `Reply rate`, `Bounce rate`, `Sender bounce rate`, and `Open rate`.
-   `Sender bounces`: bounces broken down by `Domain`, with `Bounce rate`, `Bounces`, and `Delivered` for each.

Turn on `Show individual accounts` to see the same numbers per mailbox, or use `Export CSV` to pull the table out.

### For a single campaign

Open the campaign's `Analytics` tab and find the `Deliverability` section.

-   Top-line figures: `Delivery rate`, `Sender bounce rate`, and `Recipient bounce rate`.
-   Breakdowns: the same figures by `Providers`, `Email accounts`, and `Domains`.
-   `Auth errors`: shown on the account and domain tables, and the first place to look when a campaign's sends drop off unexpectedly.

The split between the two bounce types is the most useful diagnostic on the page:

-   Sender bounces: emails rejected for reasons on your side, such as mailbox authentication or reputation problems. These point at the sending setup.
-   Recipient bounces: emails rejected because the address is bad or unreachable. These point at the lead list and the enrichment that produced it.

### When a bounce rate needs attention

Aim to keep bounce rate under 1%. That's where a healthy sending setup sits, and it's the number worth holding a campaign to.

Clay's own flag comes later, at 5%, so read 5% as the point where something needs fixing rather than a level to settle at. Clay applies that threshold once a campaign has sent at least 20 emails, measured over the trailing 30 days — or over a shorter window if you changed an A/B allocation more recently than that, since re-weighting the variants changes what's being sent.

When a live campaign crosses the threshold, a `High bounce rate` warning appears on the campaign and the campaign's creator gets an email. Dismissing the warning hides it for a week, so a campaign that's still bouncing later surfaces again rather than staying quiet.

## Rotating a burnt domain

A domain that keeps bouncing carries that reputation into everything sent from it, so the 5% signal above is worth acting on early. Pause the campaign first — it stops the sending immediately and it's also what unlocks the campaign's settings, since sender accounts can only be changed while a campaign is in `Draft` or `Paused`.

With the campaign paused, use the bounce split to decide what to fix:

-   Mostly recipient bounces: the lead list is the problem, not the domain. Tighten email verification and the waterfall upstream in Audiences, then resume.
-   Mostly sender bounces: the sending setup needs work. Check for `Auth errors` on the accounts, confirm warmup is on, and look at whether send limits were raised faster than the accounts were warmed.

### Moving to fresh domains

When a domain's sender bounces stay high after that, move the campaign onto fresh domains. To pick out which ones to replace, open `Analytics` from the `Campaigns` page and sort the `Sender bounces` table by `Bounce rate`. The table arrives unsorted, so sorting it is what brings the domains worth rotating out to the top.

From there, buy a new set of accounts, let them warm for about three weeks, then select them on the campaign's `Sender accounts` tab and resume. Warmup is the part worth planning around, so it helps to order replacements before you need them.

Two of the settings in the purchase flow stay fixed once the domains are bought: the forwarding domain and the number of inboxes on each domain. Point the forwarding domain at your real site, so a prospect curious enough to look up the sending domain lands somewhere legitimate.

**Note:** Keep the old accounts in place until the replacements are warm. Deleting an account you bought from Clay deletes every account on the same domain together, and those accounts can't be re-added afterwards.

## Why we don't recommend open and click tracking

Open and click tracking both need HTML, and HTML can negatively affect deliverability for cold outbound. That's why plaintext is the default in Clay. The numbers have also become less dependable than they used to be, now that providers such as Apple Mail prefetch images on the recipient's behalf.

Replies are the better signal, and the one worth optimizing for. A reply is unambiguous, it's the outcome you actually want, and positive reply rate tells you more about a campaign than any open rate will. Even an out-of-office auto-reply is useful, since it confirms you reached the inbox.

-   If you do need the numbers, `Track email opens` and `Track link clicks` live in the campaign's `Settings`.
-   `Opens` and `Clicks` columns appear in the deliverability tables only for campaigns that have the matching tracking enabled.
