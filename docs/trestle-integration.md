---
title: Trestle integration
source_url: https://university.clay.com/docs/trestle-integration
description: Verify phone numbers, email addresses, names, and addresses.
last_synced: 2026-04-26T01:40:48.983Z
upstream_hash: 372aa7ddbfa8b429c375a404887dc30b51ac7b73389353fd047bbf4cfa60ba30
---

# Trestle integration

Verify phone numbers, email addresses, names, and addresses.

Trestle is a data validation tool for verifying and enriching contact information, and Clay's default phone validation provider. With this integration, you can verify phone numbers, email addresses, names, and addresses, as well as get phone activity scores.

## Enriching data with Trestle

1.  While in a Clay table, click `Add enrichment` and search for `Trestle`.
2.  Under `Integrations`, select one of the Trestle options.
3.  In the modal, you will be asked to `Select Trestle account`.
    -   If you have your own account, click `+ Add account` and go through authentication. Otherwise, use the Clay provided key.

**Note:** This integration supports US and Canada phone numbers only.

### `Action` Verify contact

Verifies and grades phone numbers, emails, and addresses, delivering a phone activity score, line type, name match, and contact grade for both phone and email.

**Inputs:**

Required:

-   Full Name: The full name of the person whose contact you want to validate.
-   Phone Number: The phone number you want to validate.

Optional:

-   Email Address: The email address you want to validate.
-   Address Street: The first line of the address you want to validate.
-   Address City: The city of the address.
-   Address State Code: The state code of the address (e.g., `CA`).
-   Address Postal Code: The postal code of the address.
-   Address Country Code: The two-letter country code of the address (e.g., `US`).
-   Include Email Deliverability: Toggle on to check whether the email address is deliverable. Incurs an additional 0.6 credit cost per run.
-   Include Email Age Checks: Toggle on to retrieve the email address age score. Incurs an additional 0.6 credit cost per run.
-   Include Litigator Checks: Toggle on to check whether the phone is associated with a known litigator. Incurs an additional 0.6 credit cost per run.

**Outputs:**

-   Phone Is Valid: Whether the phone number is valid.
-   Phone Activity Score: A score indicating how recently the phone number has been active.
-   Phone Linetype: The line type of the phone number (e.g., Mobile, Landline).
-   Phone Name Match: Whether the provided name matches the phone number owner.
-   Phone Contact Grade: A grade indicating phone contact quality.
-   Email Is Valid: Whether the email address is valid.
-   Email Contact Grade: A grade indicating email contact quality.

### `Action` Validate phone number

Validates a phone number and returns carrier details and line type. Optionally includes a phone activity score and litigator risk check.

**Inputs:**

Required:

-   Phone Number: The phone number you want to validate.

Optional:

-   Country Code: The two-letter country code for the number (e.g., `US`). Defaults to US if not provided.
-   Include Activity Score: Toggle on to include a phone activity score in the response. Incurs an additional 0.6 credit cost per run.
-   Include Litigator Checks: Toggle on to check whether the phone is associated with a known litigator. Incurs an additional 0.6 credit cost per run.

**Outputs:**

-   Phone Number: The formatted phone number.
-   Is Valid: Whether the phone number is valid.
-   Activity Score: A score indicating how recently the phone number has been active.
-   Country Calling Code: The international calling code (e.g., `1` for the US).
-   Country Code: The two-letter country code (e.g., `US`).
-   Country Name: The full country name.
-   Line Type: The line type (e.g., Mobile, Landline).
-   Carrier: The phone carrier name.
-   Is Prepaid: Whether the phone number is a prepaid number.

### Run settings

-   **Auto-update:** Turn on to re-run this enrichment when input data changes. Useful for keeping phone and contact validation current as source data is refreshed.
-   **Only run if:** The enrichment will only run if conditions are met. [**Learn more about conditional formulas here!**](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101)
