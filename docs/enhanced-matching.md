---
title: Enhanced matching
description: How Enhanced matching finds hashed personal email identifiers for contact ad syncs in Clay Ads, how tiers and credits work, and what Clay sends to each ad platform.
last_synced: 2026-11-07T03:23:53.322Z
---

# Enhanced matching

Enhanced matching is Clay's hashed email enrichment: it finds the personal email identifiers ad platforms recognize, so more of your audience matches when you sync it.

Ad platforms know people by the email they signed up with, which is almost never the work email sitting in your CRM. Enhanced matching closes that gap inside Clay Ads, Clay's ad-audience product. It takes the professional profile URL or work email you already have and returns the personal identifiers a platform is most likely to recognize — hashed, so the raw address is never exposed.

Building an ad sync, the link between a segment in Clay and your ad platforms, is covered end to end in [Clay Ads](https://university.clay.com/docs/clay-ads). This page explains what the enrichment is doing underneath and how to get the most out of it.

**Note:** Enhanced matching runs on contact syncs. A company sync matches on company fields rather than on email, so it has no tier to pick.

## Why B2B audiences match poorly

Your CRM and your data warehouse are built around work identities — work emails, company domains, job titles, professional profile URLs. Consumer ad platforms are built around personal ones, because a personal address is what people sign up with. Send a list of work emails to Meta Ads and most of it lands on nothing, which is why B2B teams so often see low match rates on exactly the platforms where their buyers spend time.

Match rate is the share of an uploaded audience a platform can tie to a real user, and it caps everything downstream: reach, frequency, and cost per result. Identifier coverage is the lever that moves it.

## What a hashed email is

A hash is a one-way fingerprint of a piece of text. Run the same email through the SHA-256 hashing algorithm and you always get the same 64-character string; run the string backwards and you get nothing at all.

User email → clay@gmail.com

Hashed identifier → `ac0bb1c3be6934b6d32dc930ee763ce900b77092ca8236e5fc254e3e27c939a6`

Neither side of an audience match will show the other its list, so both sides compare fingerprints instead. You send hashed identifiers, the platform hashes its own users the same way, and an identical hash on both sides means the same email address sits on both.

Hashing itself is standardized and free — every major platform's own upload tool will do it for you. The hard part is knowing _which_ email to hash.

## How Enhanced matching picks the right email

1.  You point it at a professional profile URL, a work email, or both. Those two fields set the ceiling on coverage, so it's worth checking how well they're filled in on the segment you're syncing before you run.
2.  Clay queries several hashed-email data providers in parallel and waits for all of them, rather than stopping at the first one that returns a result.
3.  Those providers return hashes, never plaintext addresses. The personal email is never exposed — not to you, and not to Clay.
4.  Clay cross-references the results and ranks the candidates by provider consensus. A hash that more than one provider returned counts as a strong match and goes first; where no two providers agree, Clay spreads its picks across providers rather than taking them all from one.
5.  The top three land on the contact in Audiences, Clay's store of contacts and accounts, as `Hashed email 1`, `Hashed email 2`, and `Hashed email 3`.

Three identifiers rather than one, because you can't know which personal address someone used at signup — it might be their current one, an old one, or one from a provider they stopped using years ago. Each extra identifier is another chance at a match.

That's also why Enhanced matching suits this job better than an enrichment waterfall. A waterfall stops at the first provider that returns a hit, and that hit can be a perfectly valid personal email that simply isn't the one the person signed up with.

## What Clay sends to the ad platform

Hashing rules differ from destination to destination, and Clay applies each one on the way out. Map the plain values you have and let Clay format them.

-   **Values Clay hashes for you.** Anything a destination expects hashed is hashed with SHA-256 before upload, and anything it expects in the clear is left as it is.
-   **Values that are already hashed.** If a column you map already holds a SHA-256 hash, Clay passes it through untouched.
-   **The professional network ad platform gets one identifier per contact.** With Enhanced matching on, the professional network ad platform receives the top-ranked hashed email rather than all three, because a single strongest identifier keeps targeting precise there. The sync says so on screen when the professional network ad platform is one of your destinations.

Work emails are the stronger identifier on the professional network ad platform, and personal ones on every other destination, so it's worth mapping both and letting each platform take what it matches best on.

## Choosing a tier

Pick a tier under `Enhanced matching` on the `Match` stage of an ad sync.

| Tier | Data providers queried | Hashed emails returned |
| --- | --- | --- |
| Best match rates | Three | Up to three |
| Good match rates | Two | Up to three |
| None | None — enrichment is skipped | None |

The difference between the two paid tiers is provider coverage, not how many identifiers come back. Each tier shows its own credit cost per row right on the screen, so read the figure off your own workspace rather than borrowing someone else's.

| Use Best match rates when | Use Good match rates when |
| --- | --- |
| The audience gets reused across several campaigns | You're running a test or an experiment |
| It's a high-value or high-spend campaign | The audience is very large and you want to stay credit-conscious |
| You're seeding a lookalike or similar audience | It's a lower-stakes list, such as an exclusion audience |

`None` is the pick when your audience already carries the identifiers you want to send, or when you deliberately want to sync only what's already there.

## Emails you already have

Some teams already hold personal emails — from a product signup that runs on personal addresses, or hashed emails saved out of a previous tool. Those are worth sending, and sending them costs nothing.

On the `Match` stage, open `Email inputs` and point `Email and hashed email inputs` at the columns that hold them. Clay sends those values to each destination that accepts them, alongside anything Enhanced matching finds, so a contact can arrive with both your identifier and Clay's.

## What you're charged for

Two things keep enrichment spend down, and both happen on their own.

-   **You pay once per contact.** A hashed email that comes back is stored on the audience member and reused by later syncs, including a sync built from a different segment that happens to contain the same person.
-   **A contact Clay can't find a hashed email for isn't charged.** Enrichment that comes back with nothing is refunded.

## FAQs

### Can I run Enhanced matching on a Clay table?

No. It's part of an ad sync rather than a standalone enrichment you add to a table, and it writes its results onto contacts in Audiences. If you already hold hashed emails in a table, you can bring them into Audiences and map them on the `Match` stage — those steps are in [Clay Ads](https://university.clay.com/docs/clay-ads).

### Does Enhanced matching ever give me plaintext personal emails?

No. The providers behind it return hashes, so a plaintext address never reaches your workspace. That's deliberate: a hashed personal email can only be used for ad matching, which is why it costs considerably less than a plaintext one you could sequence against. If you need plaintext personal emails for outreach, that's a separate enrichment.

### Why do some contacts come back with nothing?

Enhanced matching needs at least one of a professional profile URL or a work email, so a contact holding neither is skipped before any provider is queried. Coverage is also deepest for people based in the US, and a contact sourced only from Clay's data marketplace is skipped when its country is set to anything outside the US. Filling in profile URLs and work emails on your segment is the most dependable way to lift coverage.

### Which hashed email does the professional network ad platform get?

The top-ranked one — the hash with the most provider agreement behind it. The other two stay on the contact in Audiences and still go to every other destination in the same sync, so adding the professional network ad platform to a sync doesn't cost you the other identifiers.

## Related

-   [Clay Ads](https://university.clay.com/docs/clay-ads)
-   [Meta Ads in Clay](https://university.clay.com/docs/meta-ads-in-clay)
-   [Audiences](https://university.clay.com/docs/audiences)
