---
title: Bright Data integration overview
source_url: https://university.clay.com/docs/bright-data-integration-overview
description: Web data platform providing proxies, scrapers, and datasets.
last_synced: 2026-04-27T18:09:26.562Z
upstream_hash: 8a175266aa03049d7f91cb84025bf599372980cdec1ee57c7ad263b26c7fa580
---

# Bright Data integration overview

Web data platform providing proxies, scrapers, and datasets.

## Bright Data Overview

Bright Data is an AI-powered tool that extracts specific data from any website or document by simply asking questions.

## Setting up Bright Data and Clay integration

To set up the Bright Data integration, connect your Bright Data account by adding your API key. You can access this in the **Settings > Connections** or via any integration panel.

## **Available Actions with the Bright Data Integration**

### `Action` **Trigger Realtime Data Collector**

Use this action to initiate Bright Data’s Realtime Data Collector to gather up-to-date information from web sources.

**Setup Inputs**

-   **Collector ID**: Enter or select a column containing the Collector ID of the Bright Data collector you want to trigger.
-   **Body** (Optional): Provide additional parameters in the request body if required.

### `Action` **Find Realtime Data Collector Results**

Use this action to retrieve real-time results from Bright Data’s Web Scraper IDE in Clay workflows.

**Setup Inputs**

-   **Response ID**: Enter or select a column containing the Response ID to retrieve data from the specified Bright Data collector.
