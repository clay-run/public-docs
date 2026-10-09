---
title: Sequencer FAQs and best practices
description: Answers to common questions about Clay's Sequencer cold email product, covering costs, limits, deliverability best practices, and troubleshooting steps.
last_synced: 2026-09-01T04:57:22.161Z
---

# Sequencer FAQs and best practices

Answers to common questions about Clay's Sequencer, plus the best practices that keep cold campaigns landing in the primary inbox.

Answers to common questions about Clay's Sequencer, plus the best practices that keep cold campaigns landing in the primary inbox.

Sequencer is Clay's cold email product: you attach a set of leads to a campaign — either a segment of People from Audiences or rows from a Clay table in a workbook — and Clay sends a sequence of up to four emails to every lead that enters it. This page is the catch-all for questions that span the whole product — costs and limits, behavior you can't change, and what to check when something looks off. It also collects the practices that separate campaigns landing in the inbox from campaigns that don't.

## Best practices

Five habits do most of the work here.

-   **Send emails the way you'd want to receive them.** The golden rule of outbound: your goal is the recipient's primary inbox, and a message that lands in Spam or Promotions is unlikely to be read. Whether you get there depends as much on what you write as on how you send it. Two habits carry most of the weight — keep the offer specific to the person receiving it, and be straightforward about who you are and what you want. For a deeper treatment of cold email as a craft, [Za-zu's Cold Email Handbook](https://za-zu.com/docs/handbook/intro) is the best external guide we know of.
-   **Vary your copy.** An identical message sent thousands of times is easy for spam filters to recognize and easy for recipients to spot. Vary it at the sentence level with spintax and per-lead variables, and let AI snippets write the parts that genuinely differ from lead to lead. One thing to know about spintax: it randomizes wording, but it isn't tracked as a test arm, so Clay doesn't measure which variation performed better. When you want a measurable comparison between two versions of your copy, set up an [A/B test](https://university.clay.com/docs/ab-test-sequence-copy) instead.
-   **Mimic human sending patterns.** Pace your sends the way a person would — spread across the working day with some randomness, rather than all at once. Clay defaults to a 20-minute minimum gap between emails from the same account, which is a sensible starting point. When you need more volume, add sender accounts rather than raising the per-account limit: more accounts means faster pacing across the campaign without asking any single inbox to send more than it comfortably can.
-   **Warm up before you scale.** A brand-new inbox that suddenly sends hundreds of emails looks suspicious to email providers. Warmup builds reputation gradually by exchanging mail with other inboxes, and accounts purchased in Clay take roughly three weeks to become fully warmed. Plan for about 20 emails per day per inbox and 3 inboxes per domain — 5 at the most — once you're at steady state. Keep warmup on at all times, not just during the initial ramp.
-   **Iterate across many small campaigns.** Launching locks a campaign's shape — you can edit copy and step timing while the campaign is paused, but you can't add, remove, or reorder steps, because that would break the analytics underneath. Smaller campaigns are easier to learn from for exactly that reason: you find out whether a sequence works before you've committed a large segment to it. A lead also receives only one sequence per campaign, so running several narrower campaigns leaves you room to come back later with a genuinely different angle.

**Note:** Warmup is enabled and managed for you on accounts purchased in Clay. On accounts you connect yourself it's opt-in — turn it on from the 3-dot menu next to the account, where you'll also find advanced settings like warmup emails per day.

## General FAQs

### What's the difference between table-based and segment-based campaigns?

The main difference is where leads come from. A table-based campaign syncs rows from a Clay table in a workbook; a segment-based campaign attaches a segment of People in [Audiences](https://university.clay.com/docs/audiences) and enrolls leads continuously as they enter it.

Because every lead in a segment-based campaign is an Audiences record, campaign activity writes back onto that person — and rolls up to their company — so replies and bounces become data you can segment and act on later.

|  | Table campaigns | People campaigns |
| --- | --- | --- |
| Lead source | Rows synced from a Clay table in a workbook | A segment of People in Audiences |
| Enrollment | Rows you sync into the campaign | Continuous, as leads enter the segment |
| Scale | Bounded by the size of the source table | Up to 500,000 leads per campaign |
| Activity tracking | Not available | Every event written back to the person and company in Audiences |
| Lead-level detail | The Leads tab | The Activity tab |
| Plans | All plans | Launch, Growth, and Enterprise |
| Development | New development goes into segment-based campaigns | Where new features ship |

On the `Campaigns` page, table-based campaigns are labeled `Table` and segment-based campaigns are labeled `People`.

### What happens to my existing table-based campaigns?

They keep running exactly as they do today, on every plan. Table-based campaigns stay supported, and new development is going into segment-based campaigns.

If you're starting something new, build it as a segment-based campaign. [Table-based campaigns](https://university.clay.com/docs/email-sequencer) remains the reference for the table-based flow.

### Which plans include segment-based campaigns?

Launch, Growth, and Enterprise. Table-based campaigns stay available on all plans.

Buying email accounts in Clay is a step up from there: it needs Growth or Enterprise. On Launch, connect email accounts you already own and send your campaigns from those.

### What does Sequencer cost?

Each lead enrolled in a campaign costs 1 action credit. AI snippets add data credits per lead on top of that, varying with the model you choose, and the campaign shows you an estimate before you launch.

Two things are easy to miss:

-   Relaunching a paused campaign doesn't re-charge for leads that were already sequenced.
-   Credit budgets live at the workspace level and get attached to a campaign at launch. Once a budget's limit is reached, the campaigns drawing on it stop spending credits, which stops new leads enrolling.

[Launch and manage a campaign](https://university.clay.com/docs/launch-and-manage-a-campaign) covers how to set a budget.

### How many leads can one campaign hold?

Up to 500,000. Enrollment is paced rather than everyone starting at once: Clay holds new sequence starts to 100,000 leads on any single day, as a platform-wide ceiling rather than a per-campaign setting.

In practice your sender accounts' daily limits set the real pace, well below that ceiling.

### What's the difference between a cold lead and a warm lead?

A cold lead doesn't know you or your company yet. A warm lead has replied to you, or shown interest some other way.

The distinction matters because it changes how much you can send, and from where. You can send far more email to warm leads from your main domain than you can to cold leads — which is why cold campaigns usually run from separate, brand-adjacent domains, either [purchased in Clay](https://university.clay.com/docs/buying-email-accounts) or brought in yourself.

### Is Sequencer built on Smartlead?

Yes. Smartlead is the sending infrastructure behind campaigns, and Clay provides the data, personalization, and orchestration around it. Everything is billed in Clay credits, and you don't need a Smartlead account of your own.

You can't connect your own Smartlead API key to a campaign. If you have a key, you can still use it with Clay's table enrichments.

### Can I sequence channels other than email?

Sequencer is a cold email product today — a campaign sends email, and everything in it is built around that. It isn't a sales engagement platform: there's no dialer, and no assignment of manual tasks to reps.

If your motion spans more than email, drive the other steps from campaign events. Every send, reply, and bounce lands in the campaign `Events` table, so you can trigger another tool, notify a rep, or create a task elsewhere the moment something happens. [Automate campaign events](https://university.clay.com/docs/automate-campaign-events) covers what's available there.

## Sequence FAQs

### Why is HTML turned off by default?

Cold email performs better as plaintext. Email providers filter HTML aggressively because it's the vehicle for most phishing, so an HTML message from an address the recipient has never seen before is more likely to be held back.

`Enable HTML` unlocks links, images, formatting, and open and click tracking. That trade is often worth making when you already have an email history with the recipient, and rarely worth making for cold sends — [Build your sequence](https://university.clay.com/docs/build-your-sequence) walks through the setting itself.

### Why aren't open and click tracking recommended?

`Track email opens` and `Track link clicks` both work by embedding tracked resources in the message, which is the pattern spam filters look hardest for on cold mail. They've also become unreliable: providers like Apple Mail prefetch images and follow links on the recipient's behalf, so opens get recorded for people who never saw the message.

Replies are the signal worth optimizing for. They're unambiguous, and measuring them costs you nothing in deliverability.

### What happens when a lead is out of office?

Clay recognizes out-of-office auto-replies and doesn't count them as a real reply, so one won't end a lead's sequence. If steps remain, the next one waits until after the return date stated in the auto-reply and then sends as normal — a delay rather than a recorded pause, so there's nothing for you to resume. If that date is more than 30 days out, the sequence ends for that lead.

Out-of-office replies are counted in your reply rate, and the `Reply rate` card's tooltip also shows the figure excluding them. They're tagged neutral, so they never move your positive reply rate — and they do confirm you reached the inbox, which is worth something on its own.

### Can a lead go through the same campaign twice?

No — it's one sequence per lead per campaign. Once a lead finishes or stops, that campaign is done with them.

Sequences end on their own in two ways: every email has been sent, or the lead replies. Out-of-office replies are the exception, as above.

### What's the maximum message size?

Each message in a sequence supports up to 8 KB of text. That's more room than a cold email should ever need, so the limit mainly comes up when an AI snippet is generating a whole message body and the output length isn't constrained.

### How do unsubscribes work?

With HTML enabled, `Enable unsubscribe link` appends a link to the bottom of every message, using wording you set in `Unsubscribe text`. Unsubscribes then appear alongside your other campaign metrics.

On plaintext campaigns — the default — handle it directly instead, in one of two places:

-   The `Add email to blocklist` action in the campaign `Events` table.
-   The `Blocklist` tab on the `Campaigns` page, where you add the address yourself.

Either route excludes that address from every future campaign, not just the current one.

## Lead FAQs

### Why can't I delete a lead that's already enrolled?

At enrollment a lead is handed to the sending infrastructure with its copy already generated, so there's no draft record left to remove. Pausing is the equivalent action: it stops any remaining emails to that person while the rest of the campaign keeps running, and it's reversible.

Two related behaviors are worth knowing:

-   Emails that have already gone out can't be recalled.
-   If a lead leaves the attached segment mid-sequence, `Pause lead on segment exit` pauses them for you automatically.

### I fixed a lead's data in Audiences — will their next email use it?

No. Copy is generated from the lead's Audiences data at the moment of enrollment and then frozen, AI snippets included, so every remaining email uses the data as it stood then. That's deliberate: it means a mid-sequence data change can't produce a message that contradicts the one before it.

Leads enrolled after your fix pick up the corrected data. To reach an already-enrolled person with the corrected version, pause them and enroll them in a different campaign.

### How do I send someone a second sequence?

Build a separate campaign and enroll them there — a lead can run through a given campaign's sequence only once. To control the gap between one sequence and the next, set a `Cooldown window` on each campaign and keep `Trigger cooldowns` on. A new campaign starts with no cooldown window, so until you set one nothing prevents the same person being live in two campaigns at once.

As a rule of thumb, wait a couple of months before sequencing the same person again, and only when the offer is genuinely different from the one they didn't respond to.

## Troubleshooting

**Note:** Accounts purchased in Clay are the quickest to diagnose, because Clay manages the domain, its DNS records, and the inbox directly and can trace a send end to end. The checks below apply to both sending paths.

### Emails aren't going out

Work through the most common causes first:

-   The lead's address is on the workspace `Blocklist`.
-   The lead is missing data the sequence needs — the email column itself, or a field a variable or an AI snippet reads. Those leads wait outside the sequence until the data lands, then enroll on a later run.
-   The lead is held out by the campaign's own filters: an exclusion segment, or a `Cooldown window` that an enrollment in another campaign put them inside.
-   The same address appears more than once in the campaign — a duplicate is only sequenced once.
-   A sender account is disconnected, or has hit its daily send limit.
-   The campaign is out of room on its credit budget, or its schedule window hasn't opened yet.
-   A lead is assigned to a specific sender account that's no longer selected on the campaign.

The `Activity` tab shows status per lead, including `Enrollment failed`, which usually points straight at the cause. Auth errors live elsewhere: on `Email accounts`, and on the account and domain tables in a campaign's `Deliverability` section.

### A sender account disconnected

Google and Microsoft revoke access periodically — after a stretch of inactivity, or when their own security checks flag something.

-   Reconnect the account: open `Email accounts`, find the account, and select `Reconnect` from its 3-dot menu. The item appears once the account shows `Auth error`, and reconnecting clears that status in place.
-   If it keeps failing after that, delete it and re-authenticate from scratch — the more reliable route. Accounts you connected over SMTP take that route too, since `Reconnect` covers the Google and Microsoft sign-in flows.

[Connect your own email accounts](https://university.clay.com/docs/connect-your-own-email-accounts) has the full connection flow for each method.

### Replies or events aren't appearing

Events reach Clay within five minutes for 99% of sends on accounts purchased in Clay.

-   When they're slower, it's usually the inbox: mail processing has backed up, or the inbox is briefly unreachable because of an auth error or a provider rate limit.
-   Check `Email accounts` for an `Auth error` on the account in question. That's the case you can act on — reconnect it, and the events waiting behind it come through.
-   A rate limit or a backed-up mailbox clears on its own, and the events land once it does. Pausing leads by hand doesn't speed that up.

### A test send failed

-   Retry it first — a failed test send is usually transient.
-   If it fails repeatedly, the account you picked in `Send test email` is most likely disconnected, so reconnect it and try again.

### An error appeared and the action didn't complete

-   Retry the operation. Most errors of this kind are transient, particularly anything reporting a 502.
-   If the same error keeps returning, contact support with the campaign name and roughly when it happened.
