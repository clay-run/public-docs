---
title: Google Ads in Clay
description: Sync first-party contact audiences from Clay to Google Ads Customer Match for targeting across Search, YouTube, Gmail, and Display.
last_synced: 2026-08-04T05:02:36.692Z
---

# Google Ads in Clay

Reach known contacts across Search, YouTube, Gmail, and Display with a first-party customer list synced from Clay.

Sync contact audiences from Clay to Google Ads Customer Match to reach contacts across Search, YouTube, Gmail, and the Display Network. Google Ads works with first-party data, so build these audiences from your CRM, warehouse, or a CSV.

**What you can do:**

-   Reach known contacts across Google's network, including YouTube and Gmail
-   Create exclusion lists to suppress customers and open opportunities
-   Use a customer list as the basis for Google's similar-audience expansion
-   Keep audiences current automatically as your underlying data changes

**Note:** Google Ads accepts first-party data only, and Clay applies that rule for you rather than blocking the sync — contacts whose only source is Clay's data marketplace are filtered out before upload. In `Select ad providers` the destination is labeled `For use with first-party data only.` Build the audience from your CRM, warehouse, or a CSV to get the most out of it.

## Before you connect

-   Admin access to the Google Ads account
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

Unlike Meta, Google matches acceptably on work emails as well as personal ones, so `Enhanced matching` gives a smaller lift here than it does elsewhere — though it still helps. Adding phone numbers is usually the next most valuable field.

## Google requirements

-   **1,000 matched contacts minimum** before a customer list can be used in campaigns.
-   **First-party data only.** Clay applies this for you before the sync runs, so you don't have to filter the segment yourself.

If you're below the minimum, broaden the segment, combine segments, or improve match rate with `Enhanced matching`.

## Managing your audiences

Synced audiences appear in Google Ads under audience management as a customer list, and can be used for either targeting or exclusion. Google usually finishes processing within 24 to 48 hours.

Once the list is in Google Ads you can target it on Search, YouTube, Gmail, and Display by selecting it as the audience in your campaign settings.

## FAQs

### Why were contacts dropped from my sync?

Google only accepts first-party data, so Clay filters out contacts whose only source is its own data marketplace before uploading — a contact that also came from your CRM or a CSV still goes through. The count you see synced can therefore be lower than your segment size. To maximise how many contacts reach Google, build the audience entirely from CRM or warehouse sources.

### Can I do account-based targeting on Google?

No. Google Ads supports contact-level targeting only. If you need to target everyone at a set of companies, use a professional network ads destination, which supports account-level audiences.

### My account isn't eligible for Customer Match

Customer Match becomes available once an account has enough history and is in good policy standing, and that's assessed on Google's side rather than in Clay. In the meantime, the same audience can go to your other destinations — you can add Google to a new sync once it's available.

## Troubleshooting

### The audience uploads but won't activate

Check the matched count. Google needs 1,000 matched contacts before a customer list can be used in campaigns, and Clay's `Too small` status is a narrower signal — it appears once Google reports the audience under 500. So a list between 500 and 1,000 can look healthy in Clay and still not be usable in Google. Broadening the segment or improving match rate is the fix either way.

## Related

-   [Clay Ads](https://university.clay.com/docs/clay-ads)
-   [Clay Ads compliance best practices](https://university.clay.com/docs/clay-ads-compliance-best-practices)
-   [Google's Customer Match policy](https://support.google.com/google-ads/answer/6334160)
