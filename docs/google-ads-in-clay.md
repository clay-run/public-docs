---
title: Google Ads in Clay
description: Sync contact audiences from Clay to Google Ads Customer Match to reach known contacts across Search, YouTube, Gmail, and the Display Network.
last_synced: 2026-08-24T16:53:45.494Z
---

# Google Ads in Clay

Reach known contacts across Search, YouTube, Gmail, and Display with a first-party customer list synced from Clay.

Reach known contacts across Search, YouTube, Gmail, and Display with a first-party customer list synced from Clay.

Sync contact audiences from Clay to Google Ads Customer Match to reach contacts across Search, YouTube, Gmail, and the Display Network. Google Ads works with first-party data, so build these audiences from your CRM, warehouse, or a CSV.

**What you can do:**

-   Reach known contacts across Google's network, including YouTube and Gmail
-   Create exclusion lists to suppress customers and open opportunities
-   Use a customer list as the basis for Google's similar-audience expansion
-   Keep audiences current automatically as your underlying data changes
-   ‍

**Note:** Google Ads works with first-party data only, so records you sourced from Clay's own people and company data don't qualify — records you brought from your CRM, warehouse, or a CSV do, even after you enrich them in Clay. In `Select ad providers` the destination is labeled `For use with first-party data only.`

## Before you connect

-   Admin access to the Google Ads account
-   Google sign-in for that account — Clay connects over OAuth, so basic auth with a username and password isn't supported
-   Customer Match enabled on that account — Google gates this on account history and standing, so not every account qualifies
-   An audience built entirely from first-party sources

To check eligibility, try creating a customer list in Google Ads under audience management. If the upload option is available, you're eligible.

## Connecting Google Ads to Clay

1.  Go to `Ads` in Clay and start a sync with `Create ad sync`.
2.  Choose Google Ads as a destination and authenticate with your Google account. Grant Clay permission to manage customer lists.
3.  Pick the destination from `Select account`.

The integration requests a single OAuth scope, `https://www.googleapis.com/auth/adwords`. This is the only scope Google offers for the Ads API — there's no narrower option. Clay uses it solely to create, update, and delete customer match audiences; it doesn't read campaign performance or change spend.

## How Google matches your contacts

Clay can send email, phone, first name, last name, country, and zip code.

Email, phone, first name, and last name are hashed with SHA-256 before they leave Clay. Country and zip code go up unhashed, which is what Google's matching needs. Clay also normalizes each field to the shape Google expects, so there's no need to clean the data yourself first:

-   Emails are lowercased, and on Gmail addresses Clay drops any dots and `+` suffix from the part before the @.
-   Phone numbers are stripped to digits and sent with a leading `+`, in E.164 form.
-   Names are lowercased with spaces, apostrophes, and periods removed; accents and hyphens are kept.
-   Country has to be a two-letter code, and spaces come out of zip codes.

If a column already holds SHA-256 hashes, Clay passes those straight through instead of hashing them twice.

Unlike Meta, Google matches acceptably on work emails as well as personal ones, so `Enhanced matching` gives a smaller lift here than it does elsewhere — though it still helps. Adding phone numbers is usually the next most valuable field.

## Google requirements

-   **1,000 matched contacts minimum** before a customer list can be used in campaigns.
-   **1,000,000-member maximum.** A Google sync carries up to a million members. When a single sync targets several destinations at once, the lowest maximum among them applies to the whole sync — so pairing Google with a destination that caps lower trims the list to that smaller number for every destination in the sync.
-   **First-party data only.** Records you sourced from Clay's own people and company data don't qualify; records you brought from your CRM, warehouse, or a CSV do, even after you enrich them in Clay.

If you're below the minimum, broaden the segment, combine segments, or improve match rate with `Enhanced matching`.

## Google sync settings

Two Google-specific settings appear in the sync wizard once Google Ads is one of your destinations.

**`Google Ads membership lifespan`** sits on the `Setup` stage and sets how many days a contact stays on the customer list after they were last added. Anywhere from 0 to 540 days works, and Clay starts you at 90. A shorter lifespan keeps the audience tight to recent activity; a longer one holds reach steadier between syncs.

Alongside the Google destination you'll also set `Consent for sending user data to Google` and `Consent for ad personalization`. These carry the consent signal Google requires for contacts in the EEA:

-   Set both to granted for any audience that includes EEA contacts.
-   Left unspecified, Google treats it as missing consent for those contacts.
-   Set to denied, Google rejects the upload.

Google's [EEA user consent policy](https://support.google.com/google-ads/answer/14310715) covers what you need in place before granting.

## Managing your audiences

Synced audiences appear in Google Ads under audience management as a customer list, and can be used for either targeting or exclusion. Google usually finishes processing within 24 to 48 hours.

Once the list is in Google Ads you can target it on Search, YouTube, Gmail, and Display by selecting it as the audience in your campaign settings.

## Audience size in Google Ads

Once a list finishes processing, Google reports a targetable audience size that's smaller than the number of contacts it matched. It also reports a separate size for Search, YouTube, Gmail, and Display, because a matched contact only counts toward a given size if they're eligible for that inventory type.

For the general reason matched and targetable counts diverge on every ad platform, see [Clay Ads](https://university.clay.com/docs/clay-ads). The part specific to Google is that there isn't one audience size to read — so check the number for the inventory you actually plan to run on, since a list that's comfortable on one surface can come up short on another.

## FAQs

### Why were contacts dropped from my sync?

Google only accepts first-party data, so contacts whose records came out of Clay's own people and company data are left out of the upload. Clay tells you before it happens: confirming the sync opens a dialog headed `Creating an ad sync will remove` with the number of contacts, and the Google line in it reads `Google doesn't support 3rd-party contacts.` The synced total will therefore be lower than your segment size.

Enrichment doesn't count against you. If the records came from your CRM, warehouse, or a CSV and you used Clay to add emails, phone numbers, or other attributes, they still sync — what matters is where the record originated, not what you added to it.

Syncing from a table works differently. If any column in that table sourced its records from Clay's people or company data, Google can't be picked as a destination for the table at all, and the option is disabled with `Google Ads only supports contacts sourced from first-party data.`

### Can I do account-based targeting on Google?

No. Google Ads supports contact-level targeting only. If you need to target everyone at a set of companies, use the professional network ads destination, which is the only destination offering account audiences.

### My account isn't eligible for Customer Match

Customer Match becomes available once an account has enough history and is in good policy standing, and that's assessed on Google's side rather than in Clay. In the meantime, the same audience can go to your other destinations — you can add Google to a new sync once it's available.

## Troubleshooting

### The audience uploads but won't activate

Check the matched count. Google needs 1,000 matched contacts before a customer list can be used in campaigns, and Clay's `Too small` status is a narrower signal — it appears once Google reports the audience under 500. So a list between 500 and 1,000 can look healthy in Clay and still not be usable in Google. Broadening the segment or improving match rate is the fix either way.

## Related

-   [Clay Ads](https://university.clay.com/docs/clay-ads)
-   [Clay Ads compliance best practices](https://university.clay.com/docs/clay-ads-compliance-best-practices)
-   [Google's Customer Match policy](https://support.google.com/google-ads/answer/6334160)
