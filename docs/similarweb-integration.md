---
title: SimilarWeb integration
description: Utilize SimilarWeb's powerful market intelligence data and
  competitive analysis capabilities.
last_synced: 2026-04-26T01:40:41.170Z
---

# SimilarWeb integration

Utilize SimilarWeb's powerful market intelligence data and competitive analysis capabilities.

SimilarWeb is a comprehensive digital intelligence platform that provides detailed web analytics, traffic insights, and competitive analysis tools.

With this integration, you can utilize SimilarWeb's powerful market intelligence data and competitive analysis capabilities directly within your Clay table.

## Setting up the SimilarWeb integration

1.  While in a Clay table, click`Add enrichment` and search for `SimilarWeb`.
2.  Under `Integrations`, select one of the SimilarWeb options.
3.  By default, SimilarWeb actions use Clay's managed SimilarWeb account, so you don't need your own credentials. To use your own SimilarWeb account instead, select `+ Add account` from the account dropdown and enter your SimilarWeb API key.

The `Get traffic distribution by geography` action is the exception: it requires your own SimilarWeb API key and can't run on Clay's managed SimilarWeb account.

## Do I need to add my SimilarWeb API key every time?

No. You only need to connect your SimilarWeb API key once per Clay workspace. When you add your own SimilarWeb account, either with `+ Add account` in a SimilarWeb action or from `Settings` > `Connections`, Clay saves it as a connection in your workspace. After that, you can select the same SimilarWeb account from the account dropdown in any SimilarWeb column, in any table in that workspace, without re-entering the key.

Whether your teammates can use your SimilarWeb connection depends on your plan:

-   **Non-Enterprise plans:** A new SimilarWeb connection can be used by anyone in the workspace.
-   **Enterprise plans:** A new SimilarWeb connection can only be used by the person who added it and by workspace admins until it's shared. To share it with your whole company, the connection owner or a workspace admin goes to `Settings` > `Connections`, finds the SimilarWeb connection, and sets its access to `Anyone in the workspace` (or adds specific people and groups). See [Access settings for connections](./access-settings-for-connections.md).

To have new SimilarWeb columns preselect your SimilarWeb account, a workspace admin can select `Set as default` from the `…` menu next to the SimilarWeb connection in `Settings` > `Connections`. Setting a default doesn't change existing SimilarWeb columns. For more on managing connections, see [Connections and integration accounts](./connections-and-integration-accounts.md).

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
