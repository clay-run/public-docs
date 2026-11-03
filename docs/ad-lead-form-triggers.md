---
title: Ad lead form triggers
description: Start a Clay workflow from LinkedIn and Meta lead gen form submissions to qualify, enrich, route, or write each new lead to Audiences.
last_synced: 2026-11-03T20:26:58.025Z
---

# Ad lead form triggers

Send LinkedIn and Meta lead gen form submissions into a Clay workflow, so each new lead is qualified, routed, or written to Audiences automatically.

The `Ad lead form` trigger is a workflow source that starts a run each time someone submits one of your lead gen forms on LinkedIn or Meta. Each run carries the answers the person gave plus the ad, campaign, and form the lead came from, so the rest of the workflow can act while the lead is still warm.

**Note:** Ad lead form triggers are in beta. A Workspace Admin can request access from the `Beta program` section of your workspace settings by clicking `Join beta program` — enrolling puts your workspace in line for beta features rather than switching this one on straight away.

**What you can do:**

-   Score and qualify a lead the moment the form is submitted
-   Enrich the person and their company from the email they gave you
-   Enroll the lead in the webinar or demo the ad offered
-   Send a gift or a mailer off the back of a completed form
-   Write the lead to an Audiences segment for your GTM team to pick up
-   Follow ad-sourced leads through to opportunities and closed-won deals in Audiences

Connect an ad account or page once and every lead form on it feeds the workflow, including forms you create later.

## Before you start

-   **Admin access to the LinkedIn ad account or Meta page that owns your lead gen forms.** This is what you authenticate with, and it's quicker to confirm now than midway through setup.
-   **A connection with lead gen permissions.** Lead gen reads more from the ad platform than an ad sync does, so an existing LinkedIn or Meta connection usually can't be reused. Clay will ask you to create a new one when that's the case.
-   **(Meta) Access to Business settings for your Facebook page,** so you can let Clay receive the page's leads. Three things need to be true on the Meta side first:
    -   Your Facebook page belongs to a [business portfolio](https://www.facebook.com/business/help/1710077379203657?id=180505742745347).
    -   You're [a member of that business portfolio](https://www.facebook.com/business/help/2169003770027706?id=2190812977867143), and it's the one your ad account and page are linked to.
    -   You have [full control](https://www.facebook.com/business/help/442345745885606) of both the ad account and the page as business assets.
-   **(Optional) An Audiences segment to write leads to.** Worth setting up first if you plan to hand leads to GTM Ops or track them through pipeline.

## Step 1: Add the trigger to a workflow

1.  Create a workflow, or open the one you want your leads to run through.
2.  In `Create trigger`, set `Type` to `On event`, pick `Ad lead form` under `Source`, and click `Add trigger`.
3.  In `Import new lead`, choose `LinkedIn` or `Meta`.

Each submission starts its own workflow run.

## Step 2: Connect the account and choose your forms

1.  Under `Connection`, choose a connection or add one. If the one you pick is missing lead gen permissions, Clay asks you to create a new connection — follow that prompt rather than reconnecting the existing one.
2.  Under `LinkedIn Ads account` or `Meta Ads account`, pick the ad account your forms run under.
3.  (Meta) Under `Page`, pick the Facebook page. Meta attaches lead gen forms to a page rather than to an ad account, so the page you choose decides which forms you see.
4.  Under `Lead forms`, keep `All forms`.
5.  Click `Add trigger`.

`All forms` captures every lead gen form on that ad account or page, including ones you create later. This holds on both LinkedIn and Meta. If you pick forms individually instead, you'll need to come back and add each new form, or its leads won't reach the workflow.

**Note:** A lead gen trigger runs on a connection that's shared with your workspace, so a private connection won't be accepted. Share the one you want to use from your connection settings, or add a new shared connection — either way the trigger keeps working when the person who created it is away.

## Step 3: Let Clay receive your page's leads (Meta)

Clay registers with your page as soon as you add the trigger, so there's nothing to publish first. Meta still needs you to grant Clay access to the page's leads.

1.  In Meta, open `Business settings` for the Facebook page your forms live on.
2.  Find Clay among the page's CRM integrations and authorize it.

**Note:** Until this is done the workflow looks healthy but no Meta leads arrive, so confirm it before you rely on them. It's a one-time step per page.

## Step 4: Check what comes in, then build out the rest

1.  Open `Columns` on the trigger to see the fields each submission brings in. Form answers are parsed into their own fields, so there's no code step to write.
2.  Click `Add 10 previous submissions` to load test data. Clay reads your forms' most recent submissions from the ad platform, so you can run the workflow against real leads before new ones arrive.
3.  Add the steps the lead should run through — scoring, enrichment, enrollment, or `Write to Audiences`. If you're writing to Audiences, choose `People`, pick or create a segment, and map the lead's fields onto it.
4.  Publish the workflow.

Asking Clay, our global agent, to draft the rest is often faster than adding each step by hand. A prompt like “update this workflow to qualify the lead, enrich their company from their email, and write it to Audiences” gets you a working draft to adjust.

## What comes in with each submission

| Field | What it is | Available on |
| --- | --- | --- |
| formInput | The lead's own answers — one entry per question on the form, such as name, email, company, and title. An answer to a multiple-choice question arrives as one entry with the chosen options separated by commas | LinkedIn and Meta |
| id | The ad platform's own ID for the submission | LinkedIn and Meta |
| createdTime | When the form was submitted | LinkedIn and Meta |
| provider | The ad platform the form runs on | LinkedIn and Meta |
| formId | The ad platform's ID for the form | LinkedIn and Meta |
| creativeId | The Clay form record the lead matched | LinkedIn and Meta |
| adId, adName | The ad the lead clicked | LinkedIn and Meta |
| campaignId, campaignName | The campaign the ad ran under | LinkedIn and Meta |
| isOrganic | Whether the lead came from an unpaid placement rather than a paid ad | LinkedIn and Meta |
| campaignGroupId, campaignGroupName | The campaign group the campaign sits in | LinkedIn |
| adsetId, adsetName | The ad set the ad sits in | Meta |
| platform | Where on Meta the ad was served | Meta |

The lead's answers and the ad details are separate things: `formInput` holds what the person typed, while the ad, campaign, and ad set fields describe where they came from. You can use either or both in the steps that follow.

## Recommended setup: ingest once, branch by use case

Keep the lead gen workflow itself small. A two-step workflow — the `Ad lead form` trigger followed by `Write to Audiences` — puts every lead into one segment. Build a separate workflow per use case that filters on that segment.

This matters because an ad account or page can power only one lead gen workflow at a time. Branching downstream also keeps each workflow short enough to read and fix, rather than one long workflow that does everything.

The use cases teams reach for first:

-   **Lead scoring and qualification.** Score the lead and decide whether it's worth routing to sales.
-   **Webinar or demo enrollment.** Enroll the lead in the event the ad offered.
-   **Gifting and physical mail.** Send a gift or mailer when someone completes the form.
-   **Pipeline tracking.** Follow ad-sourced leads in Audiences through to opportunities and closed-won deals.

## Limits

| Limit | What it means |
| --- | --- |
| One Clay workspace per ad account or page | A LinkedIn ad account or a Meta page can be connected for lead gen in one Clay workspace at a time. Picking one that another workspace holds returns This ad account is already connected in another Clay workspace. |
| One workflow per ad account or page | An ad account or page already feeding a workflow shows as already in use in the picker, with a link to the workflow holding it. Ingest once and branch downstream rather than adding it twice. |
| One connection per ad account or page | Once an ad account or page is connected through one connection, the same one can't be added again through a different connection or ad account in that workspace. |
| Meta is scoped to a page | Meta attaches lead gen forms to a Facebook page, so the page is what you pick and what each limit above applies to. An ad account with several pages takes one lead gen workflow per page. |

## FAQs

### Is there an ad lead form step I can add in the middle of a workflow?

No — `Ad lead form` is a trigger, so it only ever sits at the start. Everything after it is built from the same steps as any other Clay workflow, which is why a lead can go anywhere a workflow can take it.

### Can I move a lead gen trigger to a different workflow?

Yes, with one ordering detail. Remove the `Ad lead form` trigger from the first workflow and publish that workflow, then add the trigger in the second one. Until the first workflow is published without it, the ad account or page still counts as in use and the second workflow won't accept it.

### Can I type my own test row instead of loading previous submissions?

Not for this trigger. A submission has to match what the ad platform actually sends, so uploading a CSV or typing a row isn't offered — previous submissions are the test data. If your forms haven't collected anything yet you'll see `No previous submissions yet`, and the fastest fix is to submit the form yourself.

### My Meta forms aren't in the list when I pick a page

`Lead forms` reads from the page you selected, not from the whole ad account, so forms that live on a different page won't appear. Confirm your selection under `Page` first. If that page genuinely has no forms yet you'll see `No lead forms on this page`, and the trigger can't be saved until at least one exists.

## Related

-   [Clay Ads](https://university.clay.com/docs/clay-ads)
-   [LinkedIn Ads in Clay](https://university.clay.com/docs/linkedin-ads-in-clay)
-   [Meta Ads in Clay](https://university.clay.com/docs/meta-ads-in-clay)
