---
title: Meer integration
source_url: https://university.clay.com/docs/meer-integration
last_synced: 2026-04-26T01:40:21.149Z
upstream_hash: 5ec7b57af665ad019ca2e5e5111c349b156dfe9688ec12bc86818db784c16094
---

# Meer integration

Screen phone numbers against national do-not-call registries before initiating outbound calls.

The Meer integration helps you maintain Do Not Contact (DNC) compliance by screening phone numbers against national do-not-call registries before initiating outbound calls.

With this integration, you can check phone numbers against regularly updated DNC registries and receive status information to help you avoid contacting numbers on do-not-call lists.

## Using Meer in Clay

1.  While in a Clay table, click `Actions` and search for `Meer`.
2.  Under `Enrichments`, select `Screen phone number against DNC registries`.
3.  Choose to use your own Meer API key or the Clay-managed account.

### `Action` Screen phone number against DNC registries

Check if a phone number appears in National Do Not Call registries. Currently supports US (National DNC Registry), UK (TPS/CTPS) registries, Germany ([Robinsonliste.de](http://robinsonliste.de/)), and Ireland ([comreg.ie](http://comreg.ie/)) refreshed weekly. Returns DNC status and source information if found.

**Inputs**

-   **Phone Number (Required):** The phone number to check against DNC registries. Phone numbers are automatically normalized, but E.164 format is recommended (e.g., `+19199463022`).

**Output**

-   **Do Not Call:** Boolean value indicating whether the phone number is on a DNC registry (`true`) or not (`false`).
-   **Timestamp:** The date and time when the DNC status was checked.
-   **DNC List Source:** URL of the official registry where the phone number was found (if applicable).

**Pricing**

2 Clay credits per call (charged even if the number is not on the list).

**Rate Limits**

-   Clay key: 100 requests per second, 100 concurrent requests
-   User private key: 10 requests per second, 10 concurrent requests

## Compliance notes

-   You are responsible for your own compliance. Do Not Call Suppression is a risk-mitigation tool. It does not ensure compliance. It's always your job to assess your compliance obligations and ensure you meet them. For more guidance, see our [DNC compliance best practices](https://university.clay.com/docs/dnc-compliance) and [B2B email marketing best practices](https://university.clay.com/docs/direct-marketing-best-practices).
-   Clay and its third-party providers are not liable for any fines or costs associated with any DNC violations you might commit.
-   You are responsible for adding the DNC screening actions into your Clay workflows and refreshing the data in your CRM on a regular basis to avoid calling DNC numbers.
-   Clay's third-party providers may submit your company name to the applicable governing bodies for the purpose of proving that you are using a screening tool to help respect DNC rules.
-   You must have the authority to accept these terms on behalf of your organization.
