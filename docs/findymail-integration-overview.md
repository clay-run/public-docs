---
title: Findymail integration
description: Verified B2B email data for sales outreach.
last_synced: 2026-04-26T01:39:59.775Z
---

# Findymail integration

Verified B2B email data for sales outreach.

Findymail is a verified email finder and validator for B2B prospecting. Within Clay, you can use Findymail to find work emails from a name and domain, find work emails, find mobile phone numbers, and validate email addresses.

## Enriching data with Findymail

1.  While in a Clay table, click `Add enrichment` and search for `Findymail`.
2.  Under `Integrations`, select one of the Findymail actions.
3.  In the modal, you will be asked to `Select Findymail account`.
    -   If you haven't already connected your Findymail account, click `+ Add account` and enter your Findymail API key. You can find your API key at [https://app.findymail.com/user/api-tokens](https://app.findymail.com/user/api-tokens). Otherwise, use the Clay provided key.

### `Action` Find Work Email

Use this action to find a work email address for a person using their full name and company domain.

**Inputs**

-   **Full Name:** The full name of the person whose work email you are trying to find.
-   **Company Domain:** The company domain of the person whose work email you are trying to find (e.g., `clay.com`).

**Outputs**

-   **Email:** The work email address found for the person.
-   **Status:** The validity status of the email (e.g., `valid`).

**Pricing:** 2 credits per enriched cell with Clay-managed account.

### `Action` Find Work Email from Profile URL

Use this action to find a work email address for a person using their LinkedIn profile URL.

**Inputs**

-   **Personal Profile URL:** The LinkedIn URL of the person you want to find the work email for (e.g., `https://linkedin.com/in/examplename`).

**Outputs**

-   **Email:** The work email address found for the person.
-   **Status:** The validity status of the email (e.g., `valid`).

**Pricing:** 2 credits per enriched cell with Clay-managed account.

### `Action` Find Mobile Phone

Use this action to retrieve a mobile phone number associated with a LinkedIn profile URL.

**Inputs**

-   **Professional URL:** The LinkedIn profile URL of the person whose phone number you want to find (e.g., `https://linkedin.com/in/examplename`).

**Outputs**

-   **Mobile Phone:** The mobile phone number associated with the LinkedIn profile (e.g., `+19199463022`).

**Pricing:** 9 credits per enriched cell with Clay-managed account.

### `Action` Validate Email

Use this action to verify whether an email address is valid using Findymail.

**Inputs**

-   **Email:** The email address to validate.

**Outputs**

-   **Email:** The validated email address.
-   **Verified:** Whether the email address is valid (`true` or `false`).

**Pricing:** 1 credit per enriched cell with Clay-managed account.

### Run settings

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

## Troubleshooting

### "There was an error when trying to pull this email address" when using your own API key

If you see this error on Findymail cells when using your own Findymail API key — but the same rows work correctly when using Clay credits — the most likely cause is that your Findymail account has run out of credits.

When Clay sends a request to Findymail using your API key and your Findymail account balance is zero, Findymail rejects the request. Clay surfaces this as the generic message "There was an error when trying to pull this email address" rather than a specific credits error.

Clay credits work in this situation because they run on Clay's own Findymail account, which has a separate balance.

**To fix this:** Log in to your Findymail account at [https://app.findymail.com](https://app.findymail.com) and top up your credits. Once your balance is restored, re-run the failing rows in Clay.

If adding credits does not resolve the error, go to **Settings → Connections**, find your Findymail connection, and click **Reconnect** to re-enter your API key. Confirm the key is copied exactly from [https://app.findymail.com/user/api-tokens](https://app.findymail.com/user/api-tokens) with no extra spaces.

### "Rate limited by Findymail" or "Retried but failed" when using the Clay-provided key

This section applies when your Findymail columns run on the Clay-provided Findymail key (paid with Clay credits) rather than your own Findymail API key.

The Clay-provided Findymail key is shared across Clay workspaces, and Findymail applies its own request caps to it. When the shared key is busy, Findymail temporarily rejects requests and the Find Work Email or Validate Email cell shows "Rate limited by Findymail. Retrying...".

What Clay does automatically when Findymail rate-limits a request:

1.  Clay retries the request up to 5 times, 1 second apart.
2.  If every retry is still rate-limited, the cell shows **Retried but failed**.
3.  Credits for a **Retried but failed** cell are refunded automatically. See [Credit refunds](credit-refunds.md).

**Is there a per-minute or per-day limit on the Clay-provided Findymail key?** No. Clay doesn't set a fixed per-minute or per-day Findymail limit for your workspace. Whether a run gets through depends on how busy the shared key is at that moment, not on how many rows you send, so there's no batch size that's guaranteed to avoid "Rate limited by Findymail" on the Clay-provided key.

**To avoid shared-key rate limits, connect your own Findymail API key:**

1.  Copy your API key from [https://app.findymail.com/user/api-tokens](https://app.findymail.com/user/api-tokens).
2.  Open the Findymail column's settings and, under `Select Findymail account`, click `+ Add account` and paste your key.
3.  Save and re-run the affected rows.

With your own key, requests count against your Findymail account's own limits and credits, and the Find Work Email and Validate Email actions don't use Clay credits.

### Does re-running a Findymail row charge credits again?

Yes. Clay doesn't cache Findymail Find Work Email or Validate Email results, so re-running a row sends a new request to Findymail and is billed like a first run.

-   **Find Work Email:** charged again if it finds an email. If it finds no email, the credits are refunded.
-   **Validate Email:** a validation that ended in **Retried but failed** was already refunded, so re-running it is billed like a new validation.

For example, in a work email waterfall where Find Work Email found an email but the Validate Email step ended in **Retried but failed**, the validation was refunded but the Find Work Email lookup was charged as normal. Re-running that row charges the Find Work Email lookup again (2 credits on the Clay-provided key) if it finds an email again.
