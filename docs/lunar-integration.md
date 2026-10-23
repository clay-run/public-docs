---
title: Lunar.io integration
description: Use Lunar.io in Clay to find verified work email addresses and mobile phone numbers, with strong coverage in EMEA and APAC.
last_synced: 2026-09-28T16:43:58.051Z
---

# Lunar.io integration

Use Lunar.io in Clay to find verified work email addresses and mobile phone numbers, with especially strong phone coverage in EMEA and APAC.

Lunar.io is a contact data provider for work email addresses and mobile phone numbers, and its phone coverage has tested strongest in EMEA and APAC. With this integration, you can find a work email from a person's name and company domain or from their professional profile URL, and a mobile number from their professional profile URL.

## **Enriching data with Lunar.io**

1.  While in a Clay table, click `Add enrichment` and search for `Lunar.io`.
2.  Under `Integrations`, select one of the Lunar.io actions.
3.  In the modal, you will be asked to `Select Lunar.io account`.
    -   If you have your own Lunar.io account, click `+ Add account` and enter your `Lunar.io API Key`. Otherwise, use the Clay provided key.

**Note:** Both actions search for the contact while they run, so a row can take anywhere from a few seconds to about a minute to fill in, and phone searches are usually the slower of the two. The row fills in on its own once the result comes back, so you don't need to stay on the table while it works.

### `Action` Find work email

Finds a verified work email address for a person from their name and company domain, or from their professional profile URL.

**Inputs**

Under `Person identifiers`, provide one of these combinations: first and last name plus company domain; full name plus company domain; or a professional profile URL on its own.

-   **First name:** The person's first name. Use with `Last name` and `Company domain`.
-   **Last name:** The person's last name. Use with `First name` and `Company domain`.
-   **Full name:** The person's full name, as an alternative to first and last name. Use with `Company domain`.
-   **Company domain:** The domain of the company the person works at (e.g., `clay.com`). A full website URL works too.
-   **Person's professional profile URL:** The person's professional profile URL. Can be used on its own.

**Outputs**

-   **Work email:** The verified work email address Lunar.io found.
-   **Email quality:** Lunar.io's quality rating for that address (e.g., `good`).
-   **First name:** The first name of the person Lunar.io matched, so you can confirm the search landed on the right person.
-   **Last name:** The last name of the person Lunar.io matched.

### `Action` Find mobile phone

Finds a verified mobile phone number for a person from their professional profile URL.

**Inputs**

Required:

-   **Professional profile URL:** The professional profile URL of the person you want a mobile number for. It's the only identifier this action takes, so map it to a column of full profile URLs — a name or a company page won't work here.

**Outputs**

-   **Mobile phone number:** The verified mobile phone number Lunar.io found.

### Run settings

-   **Auto-update:** Useful when rows keep arriving, so new people are enriched as they land instead of waiting for you to re-run the column.
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

## **FAQs**

### Am I charged for rows where Lunar.io finds nothing?

No. When a search finishes without a match, Clay refunds the credits for that row, and the cell shows `No email found` or `No phone found` so those rows are easy to spot.

### Should I give `Find work email` a name and domain, a professional profile URL, or both?

Each option answers a slightly different question. When you include `Company domain`, the address you get back is for that person at that company. When you supply only `Person's professional profile URL`, Lunar.io uses whichever company the profile currently shows, which is the better choice when you aren't sure where someone works now.

Passing both is also fine: if one of the two values turns out to be unusable, the search runs on the other instead of failing the row.

### What happens if my own Lunar.io account runs low on credits?

When you connect your `Lunar.io API Key`, Clay reads the credit balance on that Lunar.io account and flags it when you are under 100 credits or out entirely. Rows that run against an empty account come back with an out-of-credits message, so top up in Lunar.io and re-run the column. If you would rather not track a second balance, use the Clay provided key instead.
