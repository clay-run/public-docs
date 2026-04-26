---
title: ContactLevel integration
source_url: https://university.clay.com/docs/contactlevel-integration
description: Enrich contacts in Clay with SHA-256 hashed personal email
  addresses for use in high-match ad audiences.
last_synced: 2026-04-26T01:39:48.108Z
upstream_hash: 608c702969f088863b7dd6832ff9a801ff4c74f9321b4349723a1a9c21e8f930
---

# ContactLevel integration

Enrich contacts in Clay with SHA-256 hashed personal email addresses for use in high-match ad audiences.

ContactLevel is a B2B advertising platform for targeting and engaging individual contacts across channels such as LinkedIn, Meta, and Google. With this integration, you can enrich contacts in Clay with SHA-256 hashed personal email addresses for use in high-match ad audiences.

## Enriching data with ContactLevel

1.  While in a Clay table, click `Add enrichment` and search for `ContactLevel`.
2.  Under `Integrations`, select one of the ContactLevel actions.
3.  In the modal, you will be asked to `Select ContactLevel account`.
    -   To use your own ContactLevel API key instead, click `+ Add account` and enter your API key. You can find your API key in your ContactLevel account settings.

### `Action` Find hashed emails with ContactLevel

Find SHA-256 hashed personal email addresses for a person using a LinkedIn URL, email address, or phone number as an identifier.

**Inputs**

Required (provide exactly one):

-   `Professional Profile URL`: The person's professional profile URL (e.g., `https://linkedin.com/in/examplename`). Required if email and phone are not provided.
-   `Email`: The person's email address. Required if professional profile URL and phone are not provided.
-   `Phone`: The person's phone number. Required if professional profile URL and email are not provided.

**Outputs**

-   `Hashed emails`: A list of SHA-256 hashed email addresses found for the person.
    -   `Hashed email`: An individual SHA-256 hashed email value.

### Run settings

-   `Auto-update`: Recommended when you want new rows or updated contact data to automatically re-run and refresh hashed email results.
-   `Only run if`: The enrichment will only run if conditions are met. ([Learn more about conditional formulas here](https://university.clay.com/docs/using-conditional-logic)).
