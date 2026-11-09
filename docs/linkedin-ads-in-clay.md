---
title: LinkedIn Ads in Clay
description: Sync people and company audiences from Clay to Campaign Manager, including setup, incremental syncs, matching fields, and audience size limits.
last_synced: 2026-11-09T20:59:09.961Z
---

Target B2B buyers by syncing people and account audiences from Clay to Campaign Manager.

Sync contact and company audiences from Clay to Campaign Manager for B2B ad targeting. This is the only Clay Ads destination that supports both people and account audiences.

**What you can do:**

-   Target decision-makers at your priority accounts from CRM or warehouse data
-   Build account audiences to reach everyone at a target company
-   Create exclusion lists so you stop paying to advertise to existing customers
-   Keep audiences current automatically as your underlying data changes

## Before you connect

-   A role on the ad account that can manage matched audiences — any role above viewer works, so admin and campaign manager both qualify
-   An active ad account with billing set up
-   The account you authenticate with must have access to that ad account

## Connecting to Clay

1.  Go to `Ads` in Clay, click `Create ad sync`, and pick `People` or `Companies`. This is where the audience's record type is set — `Companies` is only worth choosing for this destination, since no other destination accepts account audiences.
2.  In `Select an audience`, choose your segment from the `People list` or `Company list` tab.
3.  Under `Sync destinations`, add the integration and authenticate when prompted. Grant Clay permission to create and manage matched audiences.
4.  Pick the destination from `Select account`.

If the connection later lapses, the platform card shows `Connection issue` or `Reconnection required` — reconnect from there.

## Incremental syncs

An ad sync to this destination can send only what changed since its last run — the records that joined or left your segment — instead of re-uploading the full list each time. That makes recurring syncs faster and more reliable. Incremental syncing is rolling out gradually, so you may not see it in your workspace yet.

### Reconnect your ad platform connection

Incremental syncing needs a newer platform permission, so reconnect any connection made before it was available. You only need to do this once per connection.

1.  Navigate to `Settings` → `Connections`.
2.  Find your ad platform connection, click `...`, and choose `Reconnect`.
3.  Sign in to the platform and approve the permissions it asks for.

Every destination you add on that connection afterwards syncs incrementally. If a connection still needs reconnecting when you add it to a new sync, it shows a red warning — `Please reconnect this app account to continue.` — and its ad accounts won't load until you reconnect.

### Move an existing sync to incremental

Syncs you already have keep running as they are, re-sending the full list each run. The platform sets how an audience gets updated when Clay first creates it, so reconnecting doesn't change an audience that already exists. To move one over:

1.  Reconnect the ad platform connection, as above.
2.  In Audiences, open the menu on the segment the sync runs from and choose `Duplicate`. Each segment can feed only one ad sync, so the copy lets a new sync run alongside the old one.
3.  Create an ad sync from the copy and add the integration as a destination. Clay creates a new matched audience in Campaign Manager.
    -   Hashed emails from `Enhanced matching` are saved on your contacts, so the new sync reuses them instead of paying to find them again.
4.  Once the new audience is ready, add it to every campaign the old audience was in, for targeting or exclusion as before.

## How the platform matches your contacts

For people audiences, Clay can send email, first name, last name, company, title, and country.

For company audiences, Clay can send company name, company domain, company website, company page URL, stock symbol, city, state, company country, zip code, and up to three industries.

**Note:** Some fields have character limits. If long job titles are getting truncated, add a formula column to shorten them before you map.

Match rates depend heavily on which identifiers you send. Work emails alone typically match 60–70%. Running `Enhanced matching` to add a hashed personal email typically takes that to 90–95% on this platform.

### Why Clay sends one hashed email

Clay converts every email into a scrambled code before it uploads, so the addresses themselves aren't part of what Campaign Manager receives. `Enhanced matching` checks each contact against several data providers and returns up to three candidate personal emails, ranked by how many of those providers agree on the same address. An upload carries one row per email, so sending all three would enter the same person in the audience three times, on two addresses that fewer providers vouched for.

For this destination, Clay sends the top-ranked address only. That keeps one row per contact and your targeting on the people you picked.

Once `Enhanced matching` is on, `Hashed email 1`, `Hashed email 2`, and `Hashed email 3` all appear as locked chips under `Email and hashed email inputs`. That mapping is shared across every destination in the sync; for this destination, only `Hashed email 1` is sent.

## Platform requirements

-   **300 matched members to serve.** The platform won't run an audience smaller than that. For a people sync that re-sends the full list, Clay checks for 300 matchable records before uploading, so a sync that comes in short stops with a message telling you how many records it produced and to widen the segment or map more identifier fields. Incremental syncs and company syncs upload a smaller audience anyway, so check the segment's size before a campaign depends on it.
-   **300,000 records maximum.** Anything above the cap is trimmed, so split very large lists across separate syncs. This is the tightest cap of any destination — the others take up to 1,000,000.

## Managing your audiences

Synced audiences appear in Campaign Manager under matched audiences, and can be used for either targeting or exclusion. The platform takes about 48 hours to finish processing before the audience is usable.

## FAQs

### Why would I use an account audience instead of a contact audience?

Account audiences target everyone at a company rather than named individuals, so they reach buying-committee members you haven't identified yet. That makes them useful for account-based campaigns where coverage matters more than precision. Contact audiences are the better choice when you know exactly who you want to reach.

### My audience size on the platform doesn't match the number of contacts I sent. Why?

The platform audience size shown on the destination card is a deduped member count: the platform resolves the records you sent to member profiles and counts each person once. That usually puts it below the `Matched count` Clay reports for the same run, and records that don't resolve to a profile aren't counted at all.

### Can I sync the same audience to more than one ad account?

Yes. Within one sync, add the integration under `Sync destinations` once for each ad account. Each destination can use a different connection, which helps if you manage ads on behalf of clients.

## Troubleshooting

### The audience never leaves `Building`

Give it the full 48-hour processing window first — that's usually all it needs. If it's still there, check the segment has at least 300 matchable records. A people sync that re-sends the full list stops with an error when it's short, but an incremental or company sync uploads the smaller audience, and the platform won't serve one under 300.

### Match rates are lower than expected

This usually comes down to work emails without enrichment — running `Enhanced matching` to add a hashed personal email is the fastest way to improve it. For account audiences, company page URL and domain match far more reliably than company name alone.

## Related

-   [Clay Ads](https://university.clay.com/docs/clay-ads)
-   [Clay Ads compliance best practices](https://university.clay.com/docs/clay-ads-compliance-best-practices)
