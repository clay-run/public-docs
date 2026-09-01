---
title: Meta Ads in Clay
description: Sync contact audiences from Clay to Meta Ads to reach people on Facebook, Instagram, Messenger, and WhatsApp.
last_synced: 2026-08-04T05:01:41.310Z
---

# Meta Ads in Clay

Advertise across Facebook, Instagram, Messenger, and WhatsApp using contact audiences synced from Clay.

Sync contact audiences from Clay to Meta to advertise across Facebook, Instagram, Messenger, and WhatsApp. Meta rewards personal email data more than any other destination, so getting hashed personal emails onto your contacts matters more here than anywhere else.

**What you can do:**

-   Reach decision-makers outside of a work context, where they're using personal accounts
-   Use a Clay audience as the seed for a Meta lookalike audience
-   Create exclusion lists to suppress customers and open opportunities
-   Keep audiences current automatically as your underlying data changes

## Before you connect

-   Admin permissions in Meta Business Manager — a personal Facebook account isn't enough
-   An active Meta Ads account with billing set up
-   Access to the specific ad account you want to sync to
-   Meta's Custom Audience terms accepted on that account

**Note:** Accept Meta's Custom Audience terms before you connect — audiences can only be created on an account where they've been accepted. You'll find them in Meta Business Manager under Audiences when creating any custom audience.

## Connecting Meta Ads to Clay

1.  Go to `Ads` in Clay and start a sync with `Create ad sync`.
2.  Choose Meta Ads as a destination and authenticate with the Facebook account that has Business Manager access.
3.  Pick the destination from `Select account`.

For production workflows, use a system user token instead of OAuth — see below.

## Using a system user token

OAuth tokens expire every 60 days, and each expiry stops your recurring syncs until someone reconnects — the audience already in Meta stays in place and keeps serving, it just stops being updated. A system user token can be set never to expire and isn't tied to an individual employee's account.

1.  In your [Meta Business account](https://business.facebook.com/), go to `Business Settings` > `Accounts` > `Apps` and click `Add`.
2.  Choose `Create a new app ID`, name it, set the use case to `Other`, and the app type to `Business`. Click `Create app`.
3.  Give the app `Ads Management Standard Access` under `App Review` > `Permissions and Features`.
4.  Go to `Business Settings` > `Users` > `System users` and add a system user with `Admin` access.
5.  Use `Add assets` to assign both the app and the ad account to that system user with `Full Control` — not `Partial Access`.
6.  Select `Generate token`, choose your app, set the expiration to `Never expire`, confirm `ads_management` is selected, and generate.
7.  Copy the token immediately and store it in a password vault. Meta won't show it again.
8.  Back in Clay, choose `System User Token` when connecting Meta and paste it in.

Meta's own [system user documentation](https://www.facebook.com/business/help/503306463479099) covers this in more detail.

## How Meta matches your contacts

Clay can send email, first name, last name, gender, phone, mobile advertiser ID, country, city, state, and zip code.

Work emails alone typically match only 10–20% on Meta, because people sign up with personal addresses. Running `Enhanced matching` to add hashed personal emails typically takes that to 50–70%+. Location fields add a smaller additional lift.

## Managing your audiences

Synced audiences appear in Meta Ads Manager under audiences, and can be used for either targeting or exclusion. Meta usually finishes processing within 24 hours.

Meta reports audience sizes as ranges rather than exact counts for privacy reasons. That's expected and doesn't indicate a problem.

## FAQs

### Does this cover Instagram?

Yes. One Meta connection covers Facebook, Instagram, Messenger, and WhatsApp. Choose placements when you build the campaign in Meta Ads Manager, not in Clay.

### Can I build a lookalike audience from a Clay audience?

Yes, and it's one of the stronger plays here. Sync a tight, high-value list — your best-fit closed-won accounts, for instance — then use it as the seed for a Meta lookalike. The narrower and higher quality the seed, the better the lookalike performs.

### Is Meta worth it for B2B?

Often, yes. The catch is that it only works if you fix match rates first, which is why `Enhanced matching` is close to mandatory here rather than optional. Meta is generally stronger for awareness than for direct response in B2B.

### My OAuth connection keeps expiring

OAuth tokens last 60 days by design. Set up a system user token as described above and the problem goes away permanently.

## Troubleshooting

### The sync fails and the audience never becomes ready

Meta's Custom Audience terms are the most common explanation, and Clay surfaces this at the point you pick the ad account — either as a `Meta custom audience terms` prompt with a link to accept them, or as an unselectable account with a tooltip pointing you to your ads manager. If the terms are signed and it's still failing, confirm the ad account is in good standing.

### Match rates are under 20%

This is nearly always work emails on their own. Run `Enhanced matching`, and add phone and location fields if you have them — together they usually move the number substantially.

## Related

-   [Clay Ads](https://university.clay.com/docs/clay-ads)
-   [Clay Ads compliance best practices](https://university.clay.com/docs/clay-ads-compliance-best-practices)
