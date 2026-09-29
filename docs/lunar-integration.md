---
title: Lunar integration
description: Find verified work email addresses and mobile phone numbers for people using their name, company domain, or professional profile URL.
last_synced: 2026-09-29T00:00:00.000Z
---

# Lunar integration

Find verified work email addresses and mobile phone numbers for people using their name, company domain, or professional profile URL.

Lunar is a contact data provider that helps sales and marketing teams find verified professional contact information for B2B outreach. You can use the Clay-managed Lunar account or connect your own Lunar API key.

## Using Lunar in Clay

1. While in a Clay table, click `Add enrichment` and search for `Lunar`.
2. Under `Integrations`, select the Lunar action you want to use.
3. Choose to use your own Lunar API key or the Clay-managed account.

### `Action` Find work email

Find a verified work email address for a person given their name and company domain, or their professional profile URL.

**Inputs**

One of the following input combinations is required:

- **First name** + **Last name** + **Company domain** — the person's first name, last name, and company domain (e.g. `clay.com`).
- **Full name** + **Company domain** — the person's full name and company domain.
- **Professional profile URL** — the person's professional profile URL, like `https://www.linkedin.com/in/john-doe`. Can be used on its own.

**Output**

- **Work email:** The person's verified work email address.
- **Email quality:** Confidence indicator for the email result (e.g. `good`).
- **First name:** The person's first name as returned by Lunar.
- **Last name:** The person's last name as returned by Lunar.

You are refunded if Lunar finds no result.

### `Action` Find mobile phone

Find a verified mobile phone number for a person using their professional profile URL.

**Inputs**

- **Professional profile URL (Required):** The person's professional profile URL, like `https://www.linkedin.com/in/john-doe`.

**Output**

- **Mobile phone number:** The person's verified mobile phone number.

You are refunded if Lunar finds no result.
