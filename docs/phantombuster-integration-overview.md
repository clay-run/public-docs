---
title: Phantombuster integration
description: Data extraction platform automating web scraping and data
  collection from websites, with troubleshooting for skipped rows and partial
  imports.
last_synced: 2026-04-26T01:40:28.345Z
---

# Phantombuster integration

Data extraction platform automating web scraping and data collection from websites.

PhantomBuster is an automation platform that helps you extract data and run automated tasks. The Clay integration lets you seamlessly work with PhantomBuster data and agents.

With this integration, you can:

-   Pull data from PhantomBuster agents into Clay.
-   Push data from Clay into PhantomBuster for automated tasks.

## **Creating a table with PhantomBuster**

1.  In a workbook, click `+ Add` at the bottom.
2.  Search for `PhantomBuster` and select from the results.
3.  In the modal, you will be asked to `Select PhantomBuster account`.
    -   If you haven't already connected your PhantomBuster account, click `+ Add account` and go through authentication.

### `Source` Pull in leads

Pull your results from PhantomBuster Containers.

**Inputs**

-   **Agent ID**
-   **Only Fetch Latest Container:** Use only the latest container.
-   **Only Fetch Specified Container ID:** If the above toggle is disabled, you can specify a container ID to fetch.

## Enriching data with PhantomBuster

1.  While in a Clay table, click `Add enrichment` and search for PhantomBuster.
2.  Under `Integrations`, select one of the PhantomBuster options.
3.  In the modal, you will be asked to `Select PhantomBuster account`.
    -   If you haven't already connected your PhantomBuster account, click `+ Add account` and go through authentication.

### `Action` Pull Data

Use this action to extract data from a PhantomBuster agent's results.

**Inputs**

-   Agent ID: The ID of the PhantomBuster agent you want to pull data from
-   Only Fetch Latest Container (Optional): Enable to get only the most recent results
-   Container ID (Optional): Specify a particular container to fetch data from

### `Action` Push Data

Use this action to send data from Clay to a PhantomBuster agent for processing.

**Inputs**

-   Agent ID: The ID of the PhantomBuster agent you want to push data to
-   Agent-specific fields: Configure the required inputs based on your chosen agent

### **Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

## Troubleshooting

### Skipped rows or partial imports

If Clay imports fewer rows than expected from a PhantomBuster agent, the most common cause is PhantomBuster storing result sets as CSV file attachments.

**What happens:** When a result set is large enough that PhantomBuster stores it as a CSV file attachment, Clay's integration cannot parse that CSV and silently skips the affected container. Clay does read JSON results directly and follows `jsonUrl` links to fetch JSON data, so containers that return JSON are imported correctly.

**Workarounds:**

-   **Reduce the batch size in PhantomBuster.** Configure parameters like "Followers per launch" to smaller values so results are returned as JSON rather than stored as a CSV file attachment.
-   **Disable "Only Fetch Latest Container"** in the Pull Data action to retrieve results from multiple containers instead of only the most recent one.
-   **Export and import manually.** Download the full CSV directly from PhantomBuster and import it into Clay using the CSV import option, or via Google Sheets.

### Errors during scraping ("page crashed")

PhantomBuster may log "page crashed" errors when it encounters issues with specific records during scraping. These errors appear in PhantomBuster's run logs, not in Clay, and can result in empty columns or missing rows. Check the PhantomBuster logs to identify the affected records and contact PhantomBuster support if the issue persists.
