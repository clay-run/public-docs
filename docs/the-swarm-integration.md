---
title: The Swarm integration
description: Find intros to companies and individuals using your network.
last_synced: 2026-04-26T01:40:47.998Z
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

**Note on investment network connections:** When The Swarm surfaces a connection through an investment path, the intermediary shown may be a VC firm, PE fund, or other investor entity — not a company where either person worked. This is expected behavior: The Swarm links the target person (who works at a company in that investor's portfolio) to someone in your network through their shared investor relationship. Because investment-based paths tend to carry weaker signal than direct colleague or alumni connections, you can use Clay's filter logic on the **Connection Strength Normalized** field to deprioritize or exclude low-scoring connections from your results.

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

**Note:** When connecting to a company domain that no Clay user has previously connected to, it may take a few hours to establish the connection. During this time, you may see an "awaiting callback" status.

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

## Expanding connectors into individual rows

Each Swarm enrichment result returns a `Relationships` array. Within each relationship, a `Connections` list holds every person in your network who can facilitate an introduction — each with their name, LinkedIn URL, current company, title, and connection strength score. Up to 10 connections per relationship are returned.

A single target person (or company contact) will often have **multiple connectors** in this list. To give each connector their own row so you can enrich or reach out to them individually, use **Send row for each item in a list** in [Send Table Data](https://university.clay.com/docs/send-table-data):

1.  Click on the Swarm result cell to open the Cell details panel.
2.  Hover over the **Connections** section and click **Take action on list → Write each item to new row in other table**.
3.  Choose your destination table and select which connector fields to send (for example, `Connector Name`, `Connector LinkedIn URL`, `Connector Current Company Name`). You can also select columns from the parent row — such as the target person's name, LinkedIn URL, or current company — to include alongside each connector. This means every row in the destination table can contain both who you are trying to reach and who in your network can make the introduction.

**Common mistake:** If you manually configure Send Table Data and choose a sub-field like `Connector Name - Connections - Relationships`, only one connector is sent per row because that path points to a single indexed item, not the full list. Always select the **Connections** array as the list source to flatten all connectors into separate rows.

## Best practices

For more information about using The Swarm with Clay, check out these videos from The Swarm team:

-   [How to run a Swarm enrichment on Clay?](https://www.youtube.com/watch?v=LcLdUMSzntM)
-   [What types of relationships are being mapped?](https://www.youtube.com/watch?v=B1FKGTPjc34)
-   [How do I get a Swarm API key and bring it into Clay?](https://www.youtube.com/watch?v=4j5gmZ1nm2k)
-   [How do I improve my match results?](https://www.youtube.com/watch?v=GnYa-p1W4Gw)
