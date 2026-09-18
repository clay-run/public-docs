---
title: Bing Ads in Clay
description: How to sync Clay contact audiences to Microsoft Advertising as a customer list using email-based matching.
last_synced: 2026-09-17T19:40:16.551Z
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

-   A Microsoft Advertising developer token
-   A Microsoft Advertising user role that can manage audiences on the ad account you're syncing to. Every role except `Viewer` qualifies.
-   An audience built from first-party sources

## Getting your developer token

Clay calls the Microsoft Advertising API with a developer token that belongs to your organization rather than to Clay. Google Ads works the other way around, with Clay supplying its own token, which makes Bing Ads the one ad destination where you bring a credential of your own to the connection.

Your token lives on the [developer settings page](https://ads.microsoft.com/cc/Settings/DevSettings) in Microsoft Advertising. Requesting a new one takes `Super Admin` credentials and the `Request Token` button on that page.

Microsoft issues a universal token, so one token covers everyone in your organization who connects. Whoever holds `Super Admin` can request it once and pass it to the teammates who'll do the connecting — a developer token is an API credential only, and grants no access to any ad account on its own. Each person still needs their own role on the accounts they want to sync to.

## Connecting Bing Ads to Clay

Bing Ads is offered as an ad sync destination only. It isn't available under `Expand your reach` when you add a platform to a table-based audience, so build Bing audiences from the `Ads` surface.

Clay applies the first-party requirement for you: contacts whose only source is Clay's own data are left out of a Bing sync, and the eligibility count shown before you sync already reflects that. See [Clay Ads compliance best practices](https://university.clay.com/docs/clay-ads-compliance-best-practices) for what qualifies as first-party data.

1.  Go to `Ads` in Clay and start a sync with `Create ad sync`.
2.  Under `Sync destinations`, click `Add sync destinations`, then select Bing Ads from `Select ad providers` — it's labeled `For use with first-party data only.` in that list.
3.  Authenticate with Microsoft Advertising and supply your developer token when prompted, then pick the destination from `Select account`.

## How Bing matches your contacts

Clay sends email only. No other identifier is supported.

That single field is the most important thing to know about this destination: with no name, phone, or location alongside it, match rate comes down to email quality alone. Running `Enhanced matching` before you sync therefore does more for your results here than anywhere else in Clay Ads.

Bing is a newer destination, and `Enhanced matching` performance on it hasn't been benchmarked yet — Clay says so in the sync confirmation when Bing or Reddit are your only destinations. Expect some variance on a first run and size the segment with that in mind.

## Bing requirements

-   **1,000-member minimum.** The check runs against matched members rather than the size of your segment, so a large list with thin email coverage can still fall short. Below the floor the audience won't serve, and Clay reports `Audience is below the 1000-member serving minimum`.
-   **1,000,000-member maximum.** A Bing sync carries up to a million members. When a single sync targets several destinations, each destination's limit is applied independently.

## Managing your audiences

Synced audiences appear in the Microsoft Advertising audience library, where you attach them to campaigns.

## FAQs

### Why is my Bing match rate lower than on other platforms?

Other destinations can match on additional identifiers — Meta on phone and location, the professional network on company and title — so they have more than one route to a given contact. Bing works from email, which means email coverage is what sets the ceiling. If Bing is coming in below your other destinations on the same audience, `Enhanced matching` is the lever that will move it.

### Should I run Bing alongside Google rather than instead of it?

Usually yes. The two reach different search audiences with little overlap, and because both accept first-party data on the same terms, an audience that qualifies for one qualifies for the other. Adding Bing to an existing Google sync is close to free incremental reach.

### Why can't I select my ad account after connecting?

An account you can see but can't select is a role problem rather than a connection problem. Clay disables any account your Microsoft Advertising role can't manage audiences on, and says so under the account. Roles are granted per customer and can be narrowed to specific accounts, so access to one account in a hierarchy doesn't carry to the rest of it.

### My Bing connection says it needs reconnecting — why?

A connection missing its developer token reports as expired, because Clay can't reach the Microsoft Advertising API without one. Reconnecting and supplying the token clears it. The token carries over when you re-authenticate, so a routine reconnect won't drop it.

## Related

-   [Clay Ads](https://university.clay.com/docs/clay-ads)
-   [Clay Ads compliance best practices](https://university.clay.com/docs/clay-ads-compliance-best-practices)
