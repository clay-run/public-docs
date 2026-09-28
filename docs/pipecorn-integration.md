---
title: Pipecorn integration
description: Find verified work email addresses and mobile phone numbers using Pipecorn's waterfall across more than 20 data sources.
last_synced: 2026-09-28T16:43:58.046Z
---

# Pipecorn integration

Use Pipecorn in Clay to find verified work email addresses and mobile phone numbers for the people in your tables.

Pipecorn is a contact data provider that runs a waterfall across more than 20 underlying data sources, with especially strong coverage in Europe. With this integration, you can find a verified work email from a person's name and company, or a verified mobile phone number from their professional profile URL.

## **Enriching data with Pipecorn**

1.  While in a Clay table, click `Add enrichment` and search for `Pipecorn`.
2.  Under `Integrations`, select one of the Pipecorn actions.
3.  In the modal, you will be asked to `Select Pipecorn account`.
    -   If you have your own Pipecorn account, click `+ Add account` and enter your `Pipecorn API Key`. Otherwise, use the Clay provided key.

**Note:** Pipecorn searches its underlying sources while the action runs, so a row can take anywhere from a few seconds to about a minute to fill in. Clay keeps checking for the result in the background, so you don't need to stay on the table.

### `Action` Find work email

Finds a verified work email address for a person from their name plus a company identifier.

**Inputs**

Required:

-   **First name:** The person's first name.
-   **Last name:** The person's last name.

Under `Company identifiers`, at least one of:

-   **Company domain:** The domain of the company the person works at (e.g., `clay.com`).
-   **Company name:** The name of the company the person works at.
-   **Person's professional profile URL:** The person's professional profile URL.

**Outputs**

-   **Work email:** The verified work email address Pipecorn found.
-   **Email status:** Pipecorn's deliverability assessment of that address (e.g., `deliverable`).

### `Action` Find mobile phone

Finds a verified mobile phone number for a person from their professional profile URL.

**Inputs**

Required:

-   **Person's professional profile URL:** The profile URL of the person you want a mobile number for.

Optional, and each one helps Pipecorn match the right person:

-   **First name:** The person's first name.
-   **Last name:** The person's last name.
-   **Company domain:** The domain of the company the person works at (e.g., `clay.com`).

**Outputs**

-   **Mobile phone number:** The verified mobile number, with country code (e.g., `+33612345678`).

### Run settings

-   **Auto-update:** Useful when rows keep arriving, so new people are enriched as they land instead of waiting for you to re-run the column.
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

## **FAQs**

### What happens to rows where Pipecorn finds nothing?

When a search finishes without a result, the cell shows `No Email Found` or `No Mobile Phone Found` so those rows are easy to spot, and Clay refunds the credits for that row.

### Can I return every mobile number Pipecorn finds, not just one?

Yes. `Mobile phone number` gives you the first verified number, and the full list of numbers from that search is available in the action's output, so you can map it into a column of its own.

### What happens if my own Pipecorn account runs low on credits?

When you connect your `Pipecorn API Key`, Clay checks the enrichment credit balance on your Pipecorn account and flags it if you are running low or have run out. Rows that run against an empty account come back with an out-of-credits message, so top up in Pipecorn and re-run the column. If you would rather not manage a separate balance, use the Clay provided key instead.
