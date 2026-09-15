---
title: Email verification statuses
description: Understand the different statuses an email address can have.
last_synced: 2026-04-26T01:39:55.342Z
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
