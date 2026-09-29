---
title: Pipecorn integration
description: Find verified work email addresses and mobile phone numbers for people using their name, company domain, or professional profile URL.
last_synced: 2026-09-29T00:00:00.000Z
---

# Pipecorn integration

Find verified work email addresses and mobile phone numbers for people using their name, company domain, or professional profile URL.

Pipecorn is a contact enrichment provider that delivers verified professional email addresses and mobile phone numbers for B2B outreach. You can use the Clay-managed Pipecorn account or connect your own Pipecorn API key.

## Using Pipecorn in Clay

1. While in a Clay table, click `Add enrichment` and search for `Pipecorn`.
2. Under `Integrations`, select the Pipecorn action you want to use.
3. Choose to use your own Pipecorn API key or the Clay-managed account.

### `Action` Find work email

Find a verified work email address for a person.

**Inputs**

- **First name (Required):** The person's first name.
- **Last name (Required):** The person's last name.

At least one of the following is also required:

- **Company domain:** The person's company domain, e.g. `clay.com`.
- **Company name:** The person's company name.
- **Professional profile URL:** The person's professional profile URL, like `https://www.linkedin.com/in/johndoe`.

**Output**

- **Work email:** The person's verified work email address.
- **Email status:** Deliverability status of the returned email (e.g. `deliverable`).

You are refunded if Pipecorn finds no result.

### `Action` Find mobile phone

Find a verified mobile phone number for a person using their professional profile URL.

**Inputs**

- **Professional profile URL (Required):** The person's professional profile URL, like `https://www.linkedin.com/in/johndoe`.
- **First name (Optional):** The person's first name. Improves match accuracy.
- **Last name (Optional):** The person's last name. Improves match accuracy.
- **Company domain (Optional):** The person's company domain. Improves match accuracy.

**Output**

- **Mobile phone number:** The person's verified mobile phone number.

You are refunded if Pipecorn finds no result.
