---
title: "[Data test] Personal email providers"
source_url: https://university.clay.com/docs/data-test-methodology-personal-emails
description: Personal email finders
last_synced: 2026-04-26T01:39:51.343Z
upstream_hash: c5635a6989b9f1feffe671986a137c717452772ed73fddb09498a7ca27cff128
---

# \[Data test\] Personal email providers

Personal email finders

First, we pulled a list of 2,354 contacts who we’ve previously emailed and could confirm the email as valid.

If the email met either of these criteria, we considered it a valid email:

-   Opened
-   Replied

Then, we ran the same list through six personal email data providers in Clay, and cross-referenced their output with our source list to see how often they found an accurate match.

Here are all of the providers we tested:

-   [Nimbler](https://www.nimbler.com/)
-   [Mixrank](https://mixrank.com/)
-   [People Data Labs](https://www.peopledatalabs.com/)
-   [ContactOut](https://contactout.com/)
-   [RocketReach](https://rocketreach.co/)

We followed this specific testing methodology because we wanted to start with a list of emails we knew were 100% valid, and not catchall. Even valid emails from a tool like NeverBounce can’t be fully trusted, as they can still bounce. This way, we can know for certain how accurate our data providers in questions really were.

### Results Overview

We ran 2,354 prospects through five rounds of enrichment (meaning, we ran each of the 2,354 prospects through each data provider, a total of five times.) We enriched (or at least attempted to enrich) their information a total of 11,770 times.

Across all providers, data providers returned an email for 53% of our list, or 6,259 emails. However, that doesn’t mean all of those emails were valid.

After comparing our enriched personal email list with our valid source list, we were only able to confirm a personal email for 5,102 emails, or 43% of our total enrichment attempts. The rest were incorrect or missing emails.  

In summary:

-   We enriched 2,354 prospects across 5 providers (11,770 enrichments)
-   5,102 emails (43%) of our total attempts were confirmed valid
-   The 5 providers returned 6,259 emails (~53% coverage)

One potential bias to call out here is that a person may have multiple personal emails that they use, and our study worked on the assumption of matching 1 person to 1 correct email. But we felt this was negligible due to multiple active & response personal emails being fairly uncommon.

### Disclaimer

These results will vary greatly depending on your industry and persona. For example, data providers probably have lower coverage for IT folks at cybersecurity companies than salespeople at sales tech companies.

It’s also important to remember that these are **_all_** great data providers. Our goal here is not to knock any one provider, but rather to show a transparent report comparing providers so you can make the most informed decision. If you must only choose one provider, we want to shed some light on the best provider for you—but really, you should be using waterfalls if you can.
