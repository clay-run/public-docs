---
title: Reddit Ads in Clay
description: How to sync contact audiences from Clay to Reddit Ads as a custom audience using email and mobile advertiser ID matching.
last_synced: 2026-08-04T05:05:14.769Z
---

# Reddit Ads in Clay

Reach known contacts on Reddit with a custom audience synced from Clay.

Sync contact audiences from Clay to Reddit as a customer list custom audience. Reddit matches on hashed identifiers only, so the mapping step is narrower than most destinations.

**What you can do:**

-   Reach known contacts on Reddit alongside your search and social campaigns
-   Create exclusion lists to suppress customers and open opportunities
-   Keep audiences current automatically as your underlying data changes

**Note:** An audience needs at least 1,000 matched users before it can be used in campaigns, and audiences below that report back as too small. Custom audiences also have a six-month lifespan here, so a resync keeps long-running campaigns supplied.

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
-   **Six-month lifespan.** Custom audiences are retained for six months, and a resync brings one back.

## Managing your audiences

Synced audiences appear in Reddit Ads Manager once Reddit reports them as ready. Clay shows the audience as `Building` while Reddit processes the upload, `Ready` once matching succeeds, and `Too small` if fewer than 1,000 users matched.

## FAQs

### What affects my match rate on Reddit?

Reddit matches on email and mobile advertiser ID, with no name or location fallback, so each contact resolves on one of those two. Send mobile advertiser IDs exactly as they come from your source — reformatting them can stop them matching. And because an audience needs 1,000 matched users to be usable, start from a list comfortably above that floor.

### What happens to my audience after six months?

Custom audiences have a six-month lifespan, and your sync type decides whether that needs attention. A recurring sync refreshes the audience automatically; a one-time sync needs a manual resync to bring it back. Because the six-month clock runs independently of your data, an audience can reach the end of its lifespan while everything on your side looks healthy — so your sync type is the first thing to check.

## Related

-   [Clay Ads](https://university.clay.com/docs/clay-ads)
-   [Clay Ads compliance best practices](https://university.clay.com/docs/clay-ads-compliance-best-practices)
