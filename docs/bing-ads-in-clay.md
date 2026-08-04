---
title: Bing Ads in Clay
description: Sync contact audiences from Clay to Microsoft Advertising as customer lists to reach contacts across the Bing search network.
last_synced: 2026-08-04T05:04:20.889Z
---

# Bing Ads in Clay

Reach your contacts across Microsoft's search network with a customer list synced from Clay.

Sync contact audiences from Clay to Microsoft Advertising as a customer list. Bing Ads matches on email alone, which makes it the most enrichment-dependent destination in Clay Ads.

**What you can do:**

-   Reach known contacts across Microsoft's search network
-   Create exclusion lists to suppress customers and open opportunities
-   Keep audiences current automatically as your underlying data changes

**Note:** Bing Ads accepts first-party data only, on the same terms as Google Ads. Build the audience from your CRM, warehouse, or a CSV upload.

## Before you connect

-   Admin access to the Microsoft Advertising account
-   An audience built from first-party sources

## Connecting Bing Ads to Clay

Bing Ads is offered as an ad sync destination only. It isn't available under `Expand your reach` when you add a platform to a table-based audience, so build Bing audiences from the `Ads` surface.

Clay applies the first-party requirement for you: contacts whose only source is Clay's own data are left out of a Bing sync, and the eligibility count shown before you sync already reflects that. See [Clay Ads compliance best practices](https://university.clay.com/docs/clay-ads-compliance-best-practices) for what qualifies as first-party data.

1.  Go to `Ads` in Clay and start a sync with `Create ad sync`.
2.  Under `Sync destinations`, click `Add sync destinations`, then select Bing Ads from `Select ad providers` — it's labeled `For use with first-party data only.` in that list.
3.  Authenticate with Microsoft Advertising, then pick the destination from `Select account`.

## How Bing matches your contacts

Clay sends email only. No other identifier is supported.

That single field is the most important thing to know about this destination: with no name, phone, or location alongside it, match rate comes down to email quality alone. Running `Enhanced matching` before you sync therefore does more for your results here than anywhere else in Clay Ads.

Bing is a newer destination, and `Enhanced matching` performance on it hasn't been benchmarked yet — Clay says so in the sync confirmation when Bing or Reddit are your only destinations. Expect some variance on a first run and size the segment with that in mind.

## Bing requirements

-   **1,000-member minimum.** The check runs against matched members rather than the size of your segment, so a large list with thin email coverage can still fall short. Below the floor the audience won't serve, and Clay reports `Audience is below the 1000-member serving minimum`.

## Managing your audiences

Synced audiences appear in the Microsoft Advertising audience library, where you attach them to campaigns.

## FAQs

### Why is my Bing match rate lower than on other platforms?

Other destinations can match on additional identifiers — Meta on phone and location, LinkedIn on company and title — so they have more than one route to a given contact. Bing works from email, which means email coverage is what sets the ceiling. If Bing is coming in below your other destinations on the same audience, `Enhanced matching` is the lever that will move it.

### Should I run Bing alongside Google rather than instead of it?

Usually yes. The two reach different search audiences with little overlap, and because both accept first-party data on the same terms, an audience that qualifies for one qualifies for the other. Adding Bing to an existing Google sync is close to free incremental reach.

## Related

-   [Clay Ads](https://university.clay.com/docs/clay-ads)
-   [Clay Ads compliance best practices](https://university.clay.com/docs/clay-ads-compliance-best-practices)
