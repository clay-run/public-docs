---
title: The Swarm integration
source_url: https://university.clay.com/docs/the-swarm-integration
last_synced: 2026-04-26T01:40:47.998Z
upstream_hash: b720cbc1bb9cace978319f1e8d7c6e5ebe33278130cb6a9d8fa363a91954c73d
---

# The Swarm integration

Find intros to companies and individuals using your network.

The Swarm is a powerful networking tool that helps you discover relationship paths to companies and people.

Through this integration, you can leverage your network connections to find warm introductions to both companies and individuals.

### **How it works**

The Swarm maps relationships across three key dimensions:

-   **Professional Networks**: Identifies connections through past work experience and former colleagues
-   **Academic Connections**: Discovers alumni relationships from the same schools and graduating classes
-   **Investment Networks**: Analyzes connections through shared investors and portfolio companies

To access these powerful networking capabilities through LinkedIn, you'll need:

-   An active company Swarm account membership.
-   The Swarm Chrome extension installed on your browser.

The platform automatically updates LinkedIn connections every week, ensuring your network data stays current. Even without the Chrome extension, The Swarm continues to surface valuable connections through employment history, educational background, and investment relationships.

## **Enriching data with The Swarm**

1.  While in a Clay table, click `Add enrichment` and search for `The Swarm`.
2.  Under `Integrations`, select one of the The Swarm options.
3.  In the modal, you will be asked to `Select The Swarm account`.
    -   If you have your own account, click `+ Add account` and complete authentication. Otherwise, use the Clay provided key
        -   When using the Clay key, network mapping will be based on the company domain you provide.

**Note:** When connecting to a company domain that no Clay user has previously connected to, it may take a few hours to establish the connection. During this time, you may see an “awaiting callback” status.

### `Action` Find warm intros to person

Use this action to identify and score relationships between your company and a specific person.

**Inputs**

-   **Your company domain**
-   **Social URL:** Your target's social links.

### `Action` Find warm intros to company

Use this action to identify and score relationships between your company and a target company.

**Inputs**

-   **Your company domain**
-   **Target company domain**
-   **Job function (Optional)**
-   **Seniority (Optional):** Find intros with specific senior level titles.

### **Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

## Best practices

For more information about using The Swarm with Clay, check out these videos from The Swarm team:

-   [How to run a Swarm enrichment on Clay?](https://www.youtube.com/watch?v=LcLdUMSzntM)
-   [What types of relationships are being mapped?](https://www.youtube.com/watch?v=B1FKGTPjc34)
-   [How do I get a Swarm API key and bring it into Clay?](https://www.youtube.com/watch?v=4j5gmZ1nm2k)
-   [How do I improve my match results?](https://www.youtube.com/watch?v=GnYa-p1W4Gw)
