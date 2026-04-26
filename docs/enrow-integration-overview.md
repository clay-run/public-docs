---
title: Enrow integration
source_url: https://university.clay.com/docs/enrow-integration-overview
description: Data tool for email verification and contact finding.
last_synced: 2026-04-26T01:39:57.159Z
upstream_hash: 9dcaeced4e75725fdbb661e70ddf3c1a343ede3001955a0b8a7f24a547322b61
---

# Enrow integration

Data tool for email verification and contact finding.

Enrow is an email finding and validation tool that also provides mobile phone number lookup. In Clay, you can use Enrow to find a contact's work email, verify its deliverability, and find their mobile phone number.

## Enriching data with Enrow

1.  While in a Clay table, click `Add enrichment` and search for `Enrow`.
2.  Under `Integrations`, select one of the Enrow actions.
3.  Choose to use your own Enrow API key or the Clay-managed account.
    -   If you haven't connected an account yet, click `+ Add account` and enter your API key. You can find your API key in the `Integrations` section of your Enrow account.

### `Action` Find work email

Find a person's work email address from their name and company domain or company name.

**Inputs**

Required:

-   `Person's name`: The person's full name.

Optional:

-   `Company domain`: The person's company domain (e.g., `clay.com`). Required if `Company name` is not provided.
-   `Company name`: The person's company name (e.g., `Clay`). Required if `Company domain` is not provided.
-   `Country`: The country of the provided company (e.g., `US` or `United States of America`). Only relevant when using `Company name` instead of `Company domain`.

**Outputs**

-   `Result`:
    -   `Email`: The found work email address.
    -   `Qualification`: The email qualification status (e.g., `valid`).
    -   `Info`:
        -   `Company domain`: The company domain associated with the email.
        -   `First name`: The person's first name as interpreted by Enrow.
        -   `Last name`: The person's last name as interpreted by Enrow.

### `Action` Validate work email

Validate a person's work email address for deliverability.

**Inputs**

Required:

-   `Person's work email`: The work email address to validate (e.g., `colin@clay.com`).

**Outputs**

-   `Email`: The validated email address.
-   `Qualification`: The validation status (e.g., `valid`).
-   `ID`: A unique identifier for the validation result.

### `Action` Find mobile phone number

Find a person's mobile phone number from their professional profile URL or basic identifying information.

**Note:** You must provide either a **Professional profile URL**, or a combination of **First name**, **Last name**, and at least one of **Company name** or **Company domain**.

**Inputs**

-   `Professional profile URL`: URL of the person's professional profile (e.g., a LinkedIn URL). Required if first name, last name, and company information are not provided.
-   `First name`: The person's first name. Required if `Professional profile URL` is not provided.
-   `Last name`: The person's last name. Required if `Professional profile URL` is not provided.
-   `Company name`: The person's company name. Required if `Professional profile URL` is not provided and `Company domain` is not provided.
-   `Company domain`: The person's company domain (e.g., `clay.com`). Required if `Professional profile URL` is not provided and `Company name` is not provided.

**Outputs**

-   `Phone number`: The person's mobile phone number in international format (e.g., `+18682835770`).
-   `Qualification`: The status of the phone number result (e.g., `found`).
-   `Country`: The country code associated with the phone number (e.g., `TT`).

### Run settings

-   `Auto-update`: Automatically re-runs the enrichment when new rows are added to the table. Recommended when you are regularly adding new contacts and want enrichment to stay current.
-   `Only run if`: Only run the enrichment when certain conditions are met (e.g., when a specific column has a value).
