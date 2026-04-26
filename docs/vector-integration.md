---
title: Vector integration
source_url: https://university.clay.com/docs/vector-integration
description: Find hashed emails with Vector.
last_synced: 2026-04-26T01:40:53.258Z
upstream_hash: 7147becf7ac165d721a1bab13183bb7fdf279340f4462c144b79cf864aa35bd1
---

# Vector integration

Find hashed emails with Vector.

Vector is a contact-based advertising platform that connects B2B contact data to LinkedIn, Google, Meta, and other major ad networks. With this integration, you can find SHA-256 hashed emails for your contacts, enabling precise audience matching when building ad campaigns.

## Enriching data with Vector

1.  While in a Clay table, click `Add enrichment` and search for `Vector`.
2.  Under `Integrations`, select `Find hashed emails`.

**Note:** No account connection is required. Vector enrichments in Clay run on a Clay-managed account.

### `Action` Find hashed emails

Find SHA-256 hashed emails for a person using their professional profile URL or name and company domain.

**Note:** You must provide either a **Professional profile URL**, or a combination of **First name**, **Last name**, and **Company domain**. Providing both a profile URL and name/domain together will return the highest quality match.

**Inputs**

-   `Professional profile URL`: The person's professional profile URL (e.g., `https://www.linkedin.com/in/kareemamin/`). Required if first name, last name, and company domain are not provided.
-   `First name`: The person's first name. Required if `Professional profile URL` is not provided.
-   `Last name`: The person's last name. Required if `Professional profile URL` is not provided.
-   `Company domain`: The person's company domain (e.g., `clay.com`). Required if `Professional profile URL` is not provided.

**Outputs**

-   `SHA-256 hashed emails`: An array of SHA-256 hashed email addresses for the person.
    -   `Hash`: An individual SHA-256 hashed email value (e.g., `0843fba446eea4cfaeb851072e579fcd03d97267aba3a66637c923acfe500430`).

### Run settings

-   `Auto-update`: Automatically re-runs the enrichment when new rows are added to the table. Recommended when regularly adding new contacts to keep your ad audiences current.
-   `Only run if`: The enrichment will only run if conditions are met. \[Learn more about conditional formulas\].
