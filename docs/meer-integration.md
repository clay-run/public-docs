---
title: Meer integration
description: Screen phone numbers against national do-not-call registries before
  initiating outbound calls.
last_synced: 2026-09-24T19:43:53.173Z
---

# Meer integration

Screen phone numbers against national do-not-call registries before initiating outbound calls.

**Note:** Meer appears in the enrichment search panel for all workspaces. If your workspace has not yet accepted Meer's compliance terms, you will be prompted when you first open the integration:

-   **Workspace admins** can click **Accept terms** directly in the enrichment panel. Enter your company domain in the dialog and click **Agree and activate** to unlock Meer immediately. Admins can also accept from **Settings → Enrichments → Compliance**.
-   **Non-admins** will see a message to contact their workspace admin to accept the terms.

The Meer integration helps you maintain Do Not Contact (DNC) compliance by screening phone numbers against national do-not-call registries before initiating outbound calls.

With this integration, you can check phone numbers against regularly updated DNC registries and receive status information to help you avoid contacting numbers on do-not-call lists. Meer checks whether a phone number is on a DNC list — it does not provide or replace phone numbers.

## Using Meer in Clay

1.  While in a Clay table, click `Add enrichment` and search for `Meer`.
2.  Under `Integrations`, select `Screen phone number against DNC registries`.
3.  Choose to use your own Meer API key or the Clay-managed account.

### `Action` Screen phone number against DNC registries

Check if a phone number appears in National Do Not Call registries. Currently supports US (National DNC Registry and select state registries), UK (TPS/CTPS), Ireland ([comreg.ie](http://comreg.ie/)), Belgium (DNCM), Germany ([Robinsonliste.de](http://robinsonliste.de/)), Spain ([Lista Robinson](http://listarobinson.es)), New Zealand, and Australia, refreshed weekly. Returns DNC status and source information if found. Clay doesn't cache these results, so re-running the action screens the number again rather than replaying an earlier answer.

**Inputs**

-   **Phone Number (Required):** The phone number to check against DNC registries. E.164 format is strongly recommended for reliable results (a `+` followed by the country code and number with no spaces or dashes, e.g., `+19199463022`). Numbers in international format with spaces or dashes — such as `+1 919-946-3022` — may fail to parse and return an "Invalid input" error. To avoid this, add a **Clay Formatters → Normalize Phone Number** step and map the **E164** output field as the Meer column's **Phone Number** input.

**Output**

-   **Do Not Call:** Boolean value indicating whether the phone number is on a DNC registry (`true`) or not (`false`). A `false` result — shown as **Can call** in the Clay cell preview — means only that the number was **not found on the relevant suppression list**. It does not mean the number is legally eligible for outbound calling. Meer's screening result is a suppression signal only; it does not establish country-specific legal basis, presumed consent, or calling eligibility. Apply your own country-level calling rules and risk policies before routing numbers into call-first sequences, especially in markets such as Germany where regulations may require additional legal basis (for example, presumed consent for B2B telephone advertising) beyond registry absence.
-   **Timestamp:** The date and time when the DNC status was checked.
-   **DNC List Source:** URL of the official registry where the phone number was found (if applicable).

**Pricing**

Screening a number costs 0.6 credits per record on current Clay plans, or 0.9 credits on older plans that predate Clay's latest pricing update. You're charged whether or not the number turns out to be on a registry.

**Rate Limits**

-   Clay key: 100 requests per second, 100 concurrent requests
-   User private key: 10 requests per second, 10 concurrent requests

## Troubleshooting

-   **"Invalid input"** — the phone number could not be parsed. Make sure the number includes a country code prefix (e.g., `+19199463022`). If your numbers don't already include a country code, add a **Clay Formatters → Normalize Phone Number** step first — then update the Meer column's **Phone Number** input to reference that step's output (e.g., the **E164** field), not the original phone number column. Simply adding the normalize step without re-mapping the input will not fix the error.
-   **"Missing input"** — the Phone Number field is empty or references a column with no value. Check that the Meer action's **Phone Number** input is mapped to a column that contains data, and that any upstream normalization step completed successfully.
-   **"Error: Failed to enrich phone number"** — the phone number is valid but its country is not currently supported by Meer. Credits are not charged for this error. To avoid it entirely, add an **Only run if** conditional on this action to restrict it to supported country codes (e.g., `+1` for US, `+44` for UK, `+49` for Germany, `+353` for Ireland, `+34` for Spain).

## Compliance notes

-   You are responsible for your own compliance. Do Not Call Suppression is a risk-mitigation tool. It does not ensure compliance. It's always your job to assess your compliance obligations and ensure you meet them. For more guidance, see our [DNC compliance best practices](https://university.clay.com/docs/dnc-compliance) and [direct marketing best practices](https://university.clay.com/docs/direct-marketing-best-practices).
-   **Do Not Call = false is a suppression signal, not a call-eligibility clearance.** A result of `false` — shown as **Can call** in the Clay cell preview — means only that the number was not found on the relevant suppression list. It does not establish country-specific legal basis, presumed consent, or calling eligibility. You must apply your own country-level calling rules, particularly in markets such as Germany where B2B telephone advertising may require additional legal basis beyond registry absence.
-   Clay and its third-party providers are not liable for any fines or costs associated with any DNC violations you might commit.
-   You are responsible for adding the DNC screening actions into your Clay workflows and refreshing the data in your CRM on a regular basis to avoid calling DNC numbers.
-   Clay's third-party providers may submit your company name to the applicable governing bodies for the purpose of proving that you are using a screening tool to help respect DNC rules.
-   You must have the authority to accept these terms on behalf of your organization.
