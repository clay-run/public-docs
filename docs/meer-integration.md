---
title: Meer integration
description: Screen phone numbers against national do-not-call registries before
  initiating outbound calls.
last_synced: 2026-05-11T17:47:40.000Z
---

# Meer integration

Screen phone numbers against national do-not-call registries before initiating outbound calls.

**Important:** Meer does not appear in the enrichment search panel until you accept its compliance terms. If you cannot find Meer when adding enrichments to your table, follow these steps to unlock it:

1. Click your workspace name or the **Settings** icon
2. Navigate to **Settings → Enrichments**
3. Select the **Compliance** tab
4. Enter your company's domain when prompted, then click **Agree and activate**

Once you accept the terms, the Meer enrichment will appear in your actions panel. If you are not a workspace admin, ask your admin to complete these steps — admins will also see an **Accept terms in settings** link directly in the enrichment panel.

The Meer integration helps you maintain Do Not Contact (DNC) compliance by screening phone numbers against national do-not-call registries before initiating outbound calls.

With this integration, you can check phone numbers against regularly updated DNC registries and receive status information to help you avoid contacting numbers on do-not-call lists. Meer checks whether a phone number is on a DNC list — it does not provide or replace phone numbers.

## Using Meer in Clay

1.  While in a Clay table, click `Tools` and search for `Meer`.
2.  Under `Enrichments`, select `Screen phone number against DNC registries`.
3.  Choose to use your own Meer API key or the Clay-managed account.

### `Action` Screen phone number against DNC registries

Check if a phone number appears in National Do Not Call registries. Currently supports US (National DNC Registry), UK (TPS/CTPS), Germany ([Robinsonliste.de](http://robinsonliste.de/)), Ireland ([comreg.ie](http://comreg.ie/)), Spain ([Lista Robinson](http://listarobinson.es)), Indiana (Indiana No-Call List), Florida (Florida Do Not Call Program), Massachusetts (Massachusetts DNC Registry), and Colorado (Colorado No-Call List), refreshed weekly. Returns DNC status and source information if found.

**Inputs**

-   **Phone Number (Required):** The phone number to check against DNC registries. E.164 format is strongly recommended for reliable results (a `+` followed by the country code and number with no spaces or dashes, e.g., `+19199463022`). Numbers in international format with spaces or dashes — such as `+1 919-946-3022` — may fail to parse and return an "Invalid input" error. To avoid this, add a **Clay Formatters → Normalize Phone Number** step and map the **E164** output field as the Meer column's **Phone Number** input.

**Output**

-   **Do Not Call:** Boolean value indicating whether the phone number is on a DNC registry (`true`) or not (`false`).
-   **Timestamp:** The date and time when the DNC status was checked.
-   **DNC List Source:** URL of the official registry where the phone number was found (if applicable).

**Pricing**

2 Clay credits per call (charged even if the number is not on the list).

**Rate Limits**

-   Clay key: 100 requests per second, 100 concurrent requests
-   User private key: 10 requests per second, 10 concurrent requests

## Troubleshooting

-   **"Invalid input"** — the phone number could not be parsed. Make sure the number includes a country code prefix (e.g., `+19199463022`). If your numbers don't already include a country code, add a **Clay Formatters → Normalize Phone Number** step first — then update the Meer column's **Phone Number** input to reference that step's output (e.g., the **E164** field), not the original phone number column. Simply adding the normalize step without re-mapping the input will not fix the error.
-   **"Missing input"** — the Phone Number field is empty or references a column with no value. Check that the Meer action's **Phone Number** input is mapped to a column that contains data, and that any upstream normalization step completed successfully.
-   **"Error: Failed to enrich phone number"** — the phone number is valid but its country is not currently supported by Meer. To avoid errors and unnecessary credit charges, add an **Only run if** conditional on this action to restrict it to supported country codes (e.g., `+1` for US, `+44` for UK, `+49` for Germany, `+353` for Ireland, `+34` for Spain).

## Compliance notes

-   You are responsible for your own compliance. Do Not Call Suppression is a risk-mitigation tool. It does not ensure compliance. It's always your job to assess your compliance obligations and ensure you meet them. For more guidance, see our [DNC compliance best practices](https://university.clay.com/docs/dnc-compliance) and [B2B email marketing best practices](https://university.clay.com/docs/direct-marketing-best-practices).
-   Clay and its third-party providers are not liable for any fines or costs associated with any DNC violations you might commit.
-   You are responsible for adding the DNC screening actions into your Clay workflows and refreshing the data in your CRM on a regular basis to avoid calling DNC numbers.
-   Clay's third-party providers may submit your company name to the applicable governing bodies for the purpose of proving that you are using a screening tool to help respect DNC rules.
-   You must have the authority to accept these terms on behalf of your organization.
