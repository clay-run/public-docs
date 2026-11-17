---
title: LinkedIn Ads in Clay
description: Sync people and company audiences from Clay to Campaign Manager, including setup, incremental syncs, matching fields, matching lists that only have professional profile URLs, and audience size limits.
last_synced: 2026-11-09T20:59:09.961Z
---

Target B2B buyers by syncing people and account audiences from Clay to Campaign Manager.

## Overview

Sync contact and company audiences from Clay to LinkedIn Campaign Manager for B2B ad targeting. This is the only Clay Ads destination that supports both people and account audiences.

What you can do:

- Target decision-makers at your priority accounts from CRM or warehouse data
- Build account audiences to reach everyone at a target company
- Create exclusion lists so you stop paying to advertise to existing customers
- Keep audiences current automatically as your underlying data changes

## Before you connect

- A role on the ad account that can manage matched audiences — any role above viewer works, so admin and campaign manager both qualify
- An active LinkedIn Ads account with billing set up
- The account you authenticate with must have access to that ad account

## Connecting LinkedIn Ads to Clay

1. Go to `Ads` in Clay, click `Create ad sync`, and pick `People` or `Companies`. This is where the audience's record type is set — `Companies` is only worth choosing for LinkedIn Ads, since no other destination accepts account audiences.
2. In `Select an audience`, choose your segment from the `People list` or `Company list` tab.
3. Under `Sync destinations`, add LinkedIn Ads and authenticate when prompted. Grant Clay permission to create and manage matched audiences.
4. Pick the destination from `Select account`.

If the connection later lapses, the platform card shows `Connection issue` or `Reconnection required` — reconnect from there.

## Incremental syncs

A LinkedIn Ads sync can send only what changed since its last run — the records that joined or left your segment — instead of re-uploading the full list each time. That makes recurring syncs faster and more reliable. Incremental syncing is rolling out gradually, so you may not see it in your workspace yet.

### Reconnect your LinkedIn Ads connection

Incremental syncing needs a newer LinkedIn permission, so reconnect any connection made before it was available. You only need to do this once per connection.

1. Navigate to `Settings` → `Connections`.
2. Find your LinkedIn Ads connection, click `...`, and choose `Reconnect`.
3. Sign in to LinkedIn and approve the permissions it asks for.

Every LinkedIn Ads destination you add on that connection afterwards syncs incrementally. If a connection still needs reconnecting when you add it to a new sync, it shows a red warning — `Please reconnect this app account to continue.` — and its ad accounts won't load until you reconnect.

### Move an existing sync to incremental

Syncs you already have keep running as they are, re-sending the full list each run. LinkedIn sets how an audience gets updated when Clay first creates it, so reconnecting doesn't change an audience that already exists. To move one over:

1. Reconnect the LinkedIn Ads connection, as above.
2. In Audiences, open the menu on the segment the sync runs from and choose `Duplicate`. Each segment can feed only one ad sync, so the copy lets a new sync run alongside the old one.
3. Create an ad sync from the copy and add LinkedIn Ads as a destination. Clay creates a new matched audience in Campaign Manager.
   - Hashed emails from `Enhanced matching` are saved on your contacts, so the new sync reuses them instead of paying to find them again.
4. Once the new audience is ready, add it to every campaign the old audience was in, for targeting or exclusion as before.

## How LinkedIn matches your contacts

For people audiences, Clay can send email, first name, last name, company, title, and country.

Professional profile URLs aren't one of the identifiers Clay sends to this destination. You can pick a profile URL column in `Email and hashed email inputs` on the `Match` stage, but at upload that field only keeps valid emails and SHA-256 hashed emails, so the profile URLs are dropped rather than sent. To build a people audience from profile URLs, use `Enhanced matching` — see [My list only has professional profile URLs](#my-list-only-has-professional-profile-urls--how-do-i-match-on-them).

For company audiences, Clay can send company name, company domain, company website, company page URL, stock symbol, city, state, company country, zip code, and up to three industries.

> Note: Some fields have character limits. If long job titles are getting truncated, add a formula column to shorten them before you map.

Match rates depend heavily on which identifiers you send. Work emails alone typically match 60–70%. Running `Enhanced matching` to add a hashed personal email typically takes that to 90–95% on LinkedIn.

### Why Clay sends one hashed email

Clay converts every email into a scrambled code before it uploads, so the addresses themselves aren't part of what Campaign Manager receives. `Enhanced matching` checks each contact against several data providers and returns up to three candidate personal emails, ranked by how many of those providers agree on the same address. An upload carries one row per email, so sending all three would enter the same person in the audience three times, on two addresses that fewer providers vouched for.

For LinkedIn, Clay sends the top-ranked address only. That keeps one row per contact and your targeting on the people you picked.

Once `Enhanced matching` is on, `Hashed email 1`, `Hashed email 2`, and `Hashed email 3` all appear as locked chips under `Email and hashed email inputs`. That mapping is shared across every destination in the sync; for LinkedIn, only `Hashed email 1` is sent.

## LinkedIn requirements

- **300 matched members to serve.** LinkedIn won't run an audience smaller than that. For a people sync that re-sends the full list, Clay checks for 300 matchable records before uploading, so a sync that comes in short stops with a message telling you how many records it produced and to widen the segment or map more identifier fields. Incremental syncs and company syncs upload a smaller audience anyway, so check the segment's size before a campaign depends on it.
- **300,000 records maximum.** Anything above the cap is trimmed, so split very large lists across separate syncs. This is the tightest cap of any destination — the others take up to 1,000,000.

## Managing your audiences

Synced audiences appear in LinkedIn Campaign Manager under matched audiences, and can be used for either targeting or exclusion. LinkedIn takes about 48 hours to finish processing before the audience is usable.

## FAQs

### Why would I use an account audience instead of a contact audience?

Account audiences target everyone at a company rather than named individuals, so they reach buying-committee members you haven't identified yet. That makes them useful for account-based campaigns where coverage matters more than precision. Contact audiences are the better choice when you know exactly who you want to reach.

### My audience size in LinkedIn doesn't match the number of contacts I sent. Why?

`LinkedIn audience size` is a deduped member count: LinkedIn resolves the records you sent to member profiles and counts each person once. That usually puts it below the `Matched count` Clay reports for the same run, and records that don't resolve to a profile aren't counted at all.

### Can I sync the same audience to more than one LinkedIn ad account?

Yes. Within one sync, add LinkedIn Ads under `Sync destinations` once for each ad account. Each destination can use a different connection, which helps if you manage ads on behalf of clients.

## Troubleshooting

### The audience never leaves `Building`

Give it the full 48-hour processing window first — that's usually all it needs. If it's still there, check the segment has at least 300 matchable records. A people sync that re-sends the full list stops with an error when it's short, but an incremental or company sync uploads the smaller audience, and LinkedIn won't serve one under 300.

### Match rates are lower than expected

This usually comes down to work emails without enrichment — running `Enhanced matching` to add a hashed personal email is the fastest way to improve it. For account audiences, company page URL and domain match far more reliably than company name alone.

### My list only has professional profile URLs — how do I match on them?

An ad sync to this destination can't match on professional profile URLs directly: Clay doesn't send profile URLs to Campaign Manager, and `Email and hashed email inputs` only carries emails and SHA-256 hashed emails. If your segment has profile URLs but no emails, use `Enhanced matching` to turn the profile URLs into hashed emails that Campaign Manager can match:

1. On the `Match` stage of the ad sync, under `Enhanced matching`, pick `Good match rates` or `Best match rates`. Each tier shows its credit cost per row on screen. Enhanced matching uses each contact's professional profile URL, plus their email if they have one, to find hashed emails, and those are what Clay sends.
2. Under `Email inputs`, remove the profile URL column from `Email and hashed email inputs`. Once an Enhanced matching tier is selected, this field is no longer required, so leave it empty unless your segment has a column with real emails.
3. Under `Recommended inputs`, keep first name, last name, job title, company name, and country mapped if you have them.
4. Continue to `Sync` and send the audience.

If you'd rather not spend credits, keep `Enhanced matching` on `None` and map a column that holds real emails or SHA-256 hashed emails. With `None` selected, the `Match` stage shows `At least one email input is required.` until you map one, and profile URLs alone won't give Campaign Manager anything to match on.

### A one-time ad sync failed — how do I run it again?

A one-time ad sync that failed can't be edited or retried. To run it again, duplicate the audience segment the sync used, then create a new ad sync from the copy with the corrected `Match` settings — for example, an `Enhanced matching` tier if your segment only has professional profile URLs.

## Related

-   [Clay Ads](https://university.clay.com/docs/clay-ads)
-   [Clay Ads compliance best practices](https://university.clay.com/docs/clay-ads-compliance-best-practices)
