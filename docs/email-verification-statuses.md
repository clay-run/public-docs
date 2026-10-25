---
title: Email verification statuses
description: Understand the different statuses an email address can have, how Clay verifies emails through built-in validation providers, and how to validate a list of existing emails.
last_synced: 2026-04-26T01:39:55.232Z
---

# Email verification statuses

Understand the different statuses an email address can have.

Email verification is a key part of Clay's data enrichment capabilities. When working with contact data, having valid and active email addresses is essential for successful outreach and maintaining data quality.

Clay shows you the status of each email address through detailed verification checks, helping you focus on contacts who are most likely reachable.

-   **Valid emails are specific, active addresses** that can successfully receive emails. This status is ideal for leads, as it suggests the address is connected to a real, monitored inbox.
-   **Invalid emails do not exist.** This may come up due to a misspelling, a deactivated account, or a domain that no longer exists. These should be removed from your list to avoid bounces.
-   **Catch-all emails belong to domains that accept all email addresses**, even ones that may not be monitored or exist. While technically deliverable, these addresses don't guarantee a real inbox is behind them, making them less reliable for lead targeting. Some providers surface this domain property in their output as **Accept All** — for example, Hunter displays "Accept All: true" in a contact's cell details when the domain is catch-all. This label is a property of the domain's mail server configuration, not a verdict that the specific email address passed validation. In Clay's Work Email waterfall, the Conservative validation strategy rejects catch-all emails by default — so even when a provider finds an email on a catch-all domain, the waterfall continues searching and the final email output column stays blank. To accept catch-all results, switch to the Balanced or Aggressive validation strategy in the waterfall's Full configuration settings. See [Work Email waterfall](work-email-waterfall.md) for details.
-   **Unknown emails** couldn't be verified, often due to a temporary issue with the mail server. These might be valid, but there's no way to confirm deliverability at the moment. Retry later or proceed with caution.
-   **Role-based emails** are addresses tied to a job function (like `info@`, `sales@`, or `support@`) rather than a specific person. These are often monitored by teams, not individuals, and may lead to lower engagement.

**Note:** Email verification statuses can change over time as domains update their settings or addresses become inactive. To maintain accuracy and deliverability, it's recommended to verify your email list regularly.

## How does Clay verify an email address?

Clay doesn't run its own DNS, MX record, or SMTP checks on email addresses. Email verification in Clay runs through email validation providers that are built into Clay as enrichments. Each provider sends the email address to its own verification service and returns the result to your table. The checks each provider runs vary — for example, Hunter returns MX record, SMTP server, and SMTP check results alongside the email's status, and LeadMagic returns the domain's MX record and mail provider.

Email validation providers available in Clay include:

-   **Findymail, ZeroBounce, Hunter, Debounce, LeadMagic, Enrow, Kitt, Listmint, and Enrichley** — run on Clay credits through Clay-managed accounts, or connect your own API key.
-   **Instantly** — requires connecting your own Instantly API key.
-   **NeverBounce** — see [NeverBounce integration](neverbounce-integration-overview.md) for how to connect it.

Each provider labels its results in its own way. For example, ZeroBounce returns statuses such as `valid`, `invalid`, and `unknown` (by default, catch-all emails come back as `valid` with a `catch_all` sub-status); Debounce returns `Safe to Send`, `Invalid`, `Risky`, or `Unknown`; and Findymail returns a true/false `verified` value.

## How do I validate a list of email addresses I already have?

You can verify existing email addresses in Clay without finding new ones by running an email validation provider as a standalone enrichment:

1.  Import your email list into a Clay table (for example, from a CSV — see [CSV import](csv-import-overview.md)).
2.  Click `Add enrichment` in the top right corner and search for the validation provider you want to use (for example, `Verify email` from ZeroBounce).
3.  Choose a Clay-managed account or your own API key, map your email column as the input, and click `Save`.
4.  Run the column. Each row shows the provider's verification result for that email address.

## How do I validate emails found by the Work Email waterfall?

The Work Email waterfall can validate every email it finds and only keep emails that pass. In the waterfall's `Full configuration`, set a `Validation Provider` and choose a `Validation strategy` (`Conservative`, `Balanced`, `Aggressive`, or `Advanced`). `Conservative` is the default and excludes catch-all emails. Choose `Advanced` to decide per provider whether to `Include catch-all` and `Include unknown` results. See [Work Email waterfall](work-email-waterfall.md#validation) for details.

## Can I use an email validation provider that isn't built into Clay?

Yes. If your email validation tool offers an API — including one you already pay for — you can call it from Clay with the HTTP API enrichment. Clay sends each email address to the provider's API and writes the response to your table. See [HTTP API integration](http-api-integration-overview.md) for setup.
