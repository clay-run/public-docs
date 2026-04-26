---
title: SureConnect integration
source_url: https://university.clay.com/docs/sureconnect-integration-overview
last_synced: 2026-04-26T01:40:44.754Z
upstream_hash: 41a98b454873c8fd68a740137cd08a9dfddfaa7b84cc368fe5a437fc521121e2
---

# SureConnect integration

SureConnect identifies ‘Likely to answer’ contacts on your list, helping you increase connect rates and saving you from voicemails, gatekeepers, and dead numbers.

SureConnect helps you verify phone numbers to improve contact rates by identifying numbers that are "likely to answer." This allows you to save time by avoiding dead numbers and minimizing interaction with voicemails and gatekeepers. Results are typically returned within 2-3 hours, with a maximum wait time of one business day.

## Enriching data with SureConnect

1.  While in a Clay table, click `Add enrichment` and search for `SureConnect`.
2.  Select the `Verify Phone Number` action.
3.  In the modal, you will be asked to `Select SureConnect account`.
    -   If you haven't already connected your SureConnect account, click `+ Add account` and go through authentication. Otherwise, use the Clay provided key.

### `Action` Verify phone number

Use this action to verify if a phone number is active and likely to answer, based on SureConnect's evaluation.

**Inputs**

-   **Person's phone number:** Enter or select the column containing the phone number you want to verify
-   **Person's name:** Add the person's full name for a more accurate verification
-   **Person's company name (optional):** Specify the company name associated with the person, if available
