---
title: LinkedIn Ads in Clay
description: Sync people and company audiences from Clay to Campaign Manager, including connection steps, matching fields, record limits, and troubleshooting.
last_synced: 2026-10-20T14:56:12.865Z
---

# Professional network ads in Clay

Target B2B buyers by syncing people and account audiences from Clay to Campaign Manager.

Sync contact and company audiences from Clay to Campaign Manager for B2B ad targeting. This is the only Clay Ads destination that supports both people and account audiences.

**What you can do:**

-   Target decision-makers at your priority accounts from CRM or warehouse data
-   Build account audiences to reach everyone at a target company
-   Create exclusion lists so you stop paying to advertise to existing customers
-   Keep audiences current automatically as your underlying data changes

## Before you connect

-   A role on the ad account that can manage matched audiences — any role above viewer works, so admin and campaign manager both qualify
-   An active ad account on the professional network with billing set up
-   The account you authenticate with must have access to that ad account

## Connecting Campaign Manager to Clay

1.  Go to `Ads` in Clay, click `Create ad sync`, and pick `People` or `Companies`. This is where the audience's record type is set — `Companies` is only worth choosing for this destination, since no other destination accepts account audiences.
2.  In `Select an audience`, choose your segment from the `People list` or `Company list` tab.
3.  Under `Sync destinations`, add the professional network's ads destination and authenticate when prompted. Grant Clay permission to create and manage matched audiences.
4.  Pick the destination from `Select account`.

If the connection later lapses, the platform card shows `Connection issue` or `Reconnection required` — reconnect from there.

## How the professional network matches your contacts

For people audiences, Clay can send email, first name, last name, company, title, and country.

For company audiences, Clay can send company name, company domain, company website, company page URL, stock symbol, city, state, company country, zip code, and up to three industries.

**Note:** Some fields have character limits. If long job titles are getting truncated, add a formula column to shorten them before you map.

Match rates depend heavily on which identifiers you send. Work emails alone typically match 60–70%. Running `Enhanced matching` to add a hashed personal email typically takes that to 90–95% on the professional network.

### Why Clay sends one hashed email

Clay converts every email into a scrambled code before it uploads, so the addresses themselves aren't part of what Campaign Manager receives. `Enhanced matching` checks each contact against several data providers and returns up to three candidate personal emails, ranked by how many of those providers agree on the same address. An upload carries one row per email, so sending all three would enter the same person in the audience three times, on two addresses that fewer providers vouched for.

For this destination, Clay sends the top-ranked address only. That keeps one row per contact and your targeting on the people you picked.

Once `Enhanced matching` is on, `Hashed email 1`, `Hashed email 2`, and `Hashed email 3` all appear as locked chips under `Email and hashed email inputs`. That mapping is shared across every destination in the sync; for this destination, only `Hashed email 1` is sent.

## Professional network requirements

-   **300 matchable records minimum.** Clay checks this before uploading rather than after, so a sync that comes in short stops with a message telling you how many records it produced and to widen the segment or map more identifier fields.
-   **300,000 records maximum.** Anything above the cap is trimmed, so split very large lists across separate syncs. This is the tightest cap of any destination — the others take up to 1,000,000.

## Managing your audiences

Synced audiences appear in Campaign Manager under matched audiences, and can be used for either targeting or exclusion. The professional network takes about 48 hours to finish processing before the audience is usable.

## FAQs

### Why would I use an account audience instead of a contact audience?

Account audiences target everyone at a company rather than named individuals, so they reach buying-committee members you haven't identified yet. That makes them useful for account-based campaigns where coverage matters more than precision. Contact audiences are the better choice when you know exactly who you want to reach.

### My audience size in Campaign Manager doesn't match the number of contacts I sent. Why?

The platform's audience size is a deduped member count: the professional network resolves the records you sent to member profiles and counts each person once. That usually puts it below the `Matched count` Clay reports for the same run, and records that don't resolve to a profile aren't counted at all.

### Can I sync the same audience to more than one ad account?

Yes. Create a sync per ad account from the same Clay audience. You can also add the same platform twice within one sync if you need different authentication or destination accounts — useful if you manage ads on behalf of clients.

## Troubleshooting

### The audience never leaves `Building`

Give it the full 48-hour processing window first — that's usually all it needs. It won't be the 300-record minimum: Clay checks that before uploading, so a sync short of 300 stops with an error rather than sitting in `Building`.

### Match rates are lower than expected

This usually comes down to work emails without enrichment — running `Enhanced matching` to add a hashed personal email is the fastest way to improve it. For account audiences, company page URL and domain match far more reliably than company name alone.

## Related

-   [Clay Ads](https://university.clay.com/docs/clay-ads)
-   [Clay Ads compliance best practices](https://university.clay.com/docs/clay-ads-compliance-best-practices)
