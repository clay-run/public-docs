---
title: SimilarWeb integration
source_url: https://university.clay.com/docs/similarweb-integration
description: Utilize SimilarWeb's powerful market intelligence data and
  competitive analysis capabilities.
last_synced: 2026-04-26T01:40:41.170Z
upstream_hash: c59c31cb9c137ad73d898d470c239335a3f13b814d87d72b50b191249d2079f5
---

# SimilarWeb integration

Utilize SimilarWeb's powerful market intelligence data and competitive analysis capabilities.

SimilarWeb is a comprehensive digital intelligence platform that provides detailed web analytics, traffic insights, and competitive analysis tools.

With this integration, you can utilize SimilarWeb's powerful market intelligence data and competitive analysis capabilities directly within your Clay table.

## Setting up the SimilarWeb integration

1.  While in a Clay table, click`Add enrichment` and search for `SimilarWeb`.
2.  Under `Integrations`, select one of the Notion options.
3.  By default, you will be using your Clay-managed SimilarWeb account, but you can also select `+ Add Account` if you have your own SimilarWeb account.

## Using the SimilarWeb integration

### `Action` Find website technologies

Find the technologies that are installed on a specific website, including installation and uninstallation dates.

**Inputs**

-   **Company URL:** Select the table column that has the company domain.

**Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

### `Action` Get website visits

Show the estimated number of visits to a given domain.

**Inputs**

-   **Company URL:** Select the table column that has the company domain.
-   **Device (Optional):** Show visits only from specific devices.
-   **Country (Optional):** Show visits from a specific country.
-   **Display month (Optional):** Show visits for a specific month.
-   **Use main domain only (Optional):** Remove subdomains from the search (ex. [ads.google.com](http://ads.google.com))
-   **Use engaged visits only (Optional):** Only show engaged visits.

**Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

### `Action` Get website bounce rate

Show average bounce rate for a given domain.

**Inputs**

-   **Company URL:** Select the table column that has the company domain.

**Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

### `Action` Get traffic distribution by geography

Show traffic share, visits, pages per visit, average visit duration, and bounce rate for a given domain.

**Inputs**

-   **Company URL:** Select the table column that has the company domain.

**Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

### `Action` Get website average visit duration

Show the average visit duration for a given domain.

**Inputs**

-   **Company URL:** Select the table column that has the company domain.

**Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

### `Action` Get website pages per visit

Show the average pages per visit for a given domain.

**Inputs**

-   **Company URL:** Select the table column that has the company domain.

**Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))
