---
title: Bitly integration
source_url: https://university.clay.com/docs/bitly-integration
last_synced: 2026-04-26T01:39:42.272Z
upstream_hash: 2ca16db8096abf49a3ad8b88e03cefbf827dbcec1635751ba57e279237e19618
---

# Bitly integration

Modify your Bitly links from within Clay.

Bitly is a link management platform that lets you create and customize shortened URLs.

With this integration, you can customize your Bitly links by modifying their back-half, adding tags, and updating other link properties directly from your Clay table.

## Setting up the Bitly integration

**_Note:_** _This integration requires a Bitly API key._

1.  While in a Clay table, click `Add enrichment` and search for `Bitly`.
2.  Under `Integrations`, select `Customize link`.
3.  In the modal, you will be asked to `+ Add account`.

## Using the Bitly integration

### `Action` Customize Link

Customize and update Bitly link properties

**Inputs**

-   **Long URL:** The full destination URL you want to shorten.
-   **Group:** Select the group under which you want to create or manage this link.
-   **Domain:** Select the domain for your custom short link.
-   **Custom Slug (Optional):** Define a custom portion (slug) that replaces the automatically generated back-half of your shortened link.

**Run settings**

-   **Auto-update:** Enable automatic runs of this column.
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))
