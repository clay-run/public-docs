---
title: Reddit Ads in Clay
description: How to sync contact audiences from Clay to Reddit Ads as a custom audience using email and mobile advertiser ID matching.
last_synced: 2026-08-06T01:45:02.860Z
---

# Reddit Ads in Clay

Reach known contacts on Reddit with a custom audience synced from Clay.

Reach known contacts on Reddit with a custom audience synced from Clay.

Sync contact audiences from Clay to Reddit as a customer list custom audience. Reddit matches on hashed identifiers only, so the mapping step is narrower than most destinations.

**What you can do:**

-   Reach known contacts on Reddit alongside your search and social campaigns
-   Create exclusion lists to suppress customers and open opportunities
-   Keep audiences current automatically as your underlying data changes

**Note:** An audience needs at least 1,000 matched users before it can be used in campaigns, and audiences below that report back as too small. Reddit also retains a custom audience for a year after its last update, so a recurring sync keeps long-running campaigns supplied.

## Before you connect

-   Access to a Reddit ad account
-   The business that ad account belongs to — Reddit nests ad accounts under a business

## Connecting Reddit Ads to Clay

Reddit Ads is offered as an ad sync destination only. It isn't available under `Expand your reach` when you add a platform to a table-based audience, so build Reddit audiences from the `Ads` surface.

1.  Go to `Ads` in Clay and start a sync with `Create ad sync`.
2.  Under `Sync destinations`, click `Add sync destinations`, select Reddit Ads from `Select ad providers`, and authenticate with Reddit.
3.  Choose the business the ad account belongs to, then the ad account itself. Both selections are required before Clay can create the audience.

## How Reddit matches your contacts

Clay can send email and mobile advertiser ID only. Name, phone, company, and location fields aren't supported.

Both identifiers are hashed with SHA-256 before they leave Clay. Reddit's email normalization follows a specific set of rules: the address is lowercased, anything between `+` and `@` is dropped, and remaining non-alphanumeric characters are removed from the local part before hashing. Clay applies this for you, so a Gmail-style alias still matches correctly. Values you supply already hashed pass through untouched.

Mobile advertiser IDs need to arrive in their original format — Clay sends values in standard UUID form, so anything in another format won't make it into the sync. Case is significant too — iOS IDs are conventionally uppercase and Android's lowercase, and the same ID in different case hashes differently. Clay sends the case your data already has rather than normalizing it, so avoid reformatting the column upstream.

With only two identifiers available and no name fallback, `Enhanced matching` does most of the work on match rate here.

Reddit is a newer destination, and `Enhanced matching` performance on it hasn't been benchmarked yet — Clay says so in the sync confirmation when Reddit or Bing are your only destinations. Expect some variance on a first run and size the segment with that in mind.

## Reddit requirements

-   **1,000 matched users minimum** before the audience can be used in campaigns.
-   **1,000,000-member maximum.** A Reddit sync carries up to a million members. When a single sync targets several destinations at once, the lowest maximum among them applies to the whole sync.
-   **One-year lifespan.** Reddit retains a custom audience for one year after its last update, so every sync that updates the audience resets the clock.

## Managing your audiences

Synced audiences appear in Reddit Ads Manager once Reddit reports them as ready. Clay shows the audience as `Building` while Reddit processes the upload, `Ready` once matching succeeds, and `Too small` if fewer than 1,000 users matched.

Those statuses describe Reddit's side of the work. Clay finishes its own part first — assembling the segment, hashing identifiers, and uploading the list — and Reddit then matches that list against its users, which usually accounts for most of the wait. The audience isn't available to campaigns until Reddit reports it `Ready`, so when a sync looks slow, check which of the two stages you're waiting on before changing anything in Clay.

Audiences carry the name you give the sync, which defaults to the name of the Clay segment they came from. Naming your segments the way you want them to appear before you sync keeps them easy to pick out and report on across ad accounts in Reddit Ads Manager.

An audience that has passed its one-year lifespan doesn't get a status of its own — it reads as `Processing`. So if a long-running campaign goes quiet and the audience shows `Processing` long after the upload finished, check when it last updated before digging into the sync itself.

## FAQs

### What affects my match rate on Reddit?

Reddit matches on email and mobile advertiser ID, with no name or location fallback, so each contact resolves on one of those two. Send mobile advertiser IDs exactly as they come from your source — reformatting them can stop them matching. And because an audience needs 1,000 matched users to be usable, start from a list comfortably above that floor. Clay's testing on Reddit produced match rates between 20% and 50%, which is a reasonable range to plan a first segment around.

### What keeps my audience from expiring?

Reddit's one-year retention runs from the audience's last update, so your sync type decides whether expiry needs attention at all. A recurring sync updates the audience each time it runs and resets the clock with it, which keeps the audience available for as long as the sync stays on. A one-time sync leaves the clock running from that single upload, so an audience you synced once and left alone will reach the end of its year and need a manual resync to come back.

## Related

-   [Clay Ads](https://university.clay.com/docs/clay-ads)
-   [Clay Ads compliance best practices](https://university.clay.com/docs/clay-ads-compliance-best-practices)
