---
title: Lunar.io integration
description: Find verified work emails and mobile phone numbers with Lunar.io, with tested strength in EMEA and APAC phone coverage.
last_synced: 2026-09-29T00:00:00.000Z
---

# Lunar.io integration

Find verified work emails and mobile phone numbers with Lunar.io, with tested strength in EMEA and APAC phone coverage.

Lunar.io is a contact data provider specializing in EMEA and APAC coverage. With this integration you can find a person's verified work email or mobile phone number from their name, company domain, or professional profile URL.

## Using Lunar.io in Clay

1.  While in a Clay table, click `Add enrichment` and search for `Lunar.io`.
2.  Under `Integrations`, select one of the Lunar.io actions.
3.  In the modal, you will be asked to `Select Lunar.io account`.
    -   You can use the Clay-managed Lunar.io account, or bring your own key.
    -   To bring your own, click `+ Add account` and enter your Lunar.io API key.

### `Action` Find work email

Finds a verified work email address for a person, given their name and company domain, or their professional profile URL.

**Inputs**

One of the following input combinations is required:

-   **First name + Last name + Company domain**
-   **Full name + Company domain**
-   **Professional profile URL** (e.g. `https://www.linkedin.com/in/john-doe`) — can be used on its own

### `Action` Find mobile phone

Finds a verified mobile phone number for a person, given their professional profile URL.

**Inputs**

-   **Professional profile URL (Required):** Person's professional profile URL, e.g. `https://www.linkedin.com/in/john-doe`.
