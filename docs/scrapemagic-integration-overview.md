---
title: ScrapeMagic integration
source_url: https://university.clay.com/docs/scrapemagic-integration-overview
last_synced: 2026-04-26T01:40:37.942Z
upstream_hash: de64f539c61495e37b7f0526b77d3415c52ba3d8805fa6fdc331652683752ea6
---

# ScrapeMagic integration

AI-powered data extraction from websites and documents via questions.

## ScrapeMagic Overview

ScrapeMagic is an AI-powered tool that extracts specific data from any website or document by simply asking questions.

## Setting up ScrapeMagic and Clay integration

To set up the ScrapeMagic integration, connect your ScrapeMagic account by adding your API key. You can access this in the **Settings > Connections** or via any integration panel.

## **Available Actions with the ScrapeMagic Integration**

### `Action` **Parse Data from URL**

Use this action to extract structured data from a web page URL within Clay workflows using ScrapeMagic.

**Setup Inputs**

-   **URL**: Enter or select a column containing the URL from which you want to extract data.
-   **Fields to Extract**: Define the fields you want to extract. Enter a field name on the left and a description of the field on the right to specify what ScrapeMagic should retrieve (e.g., “sqft → The amount of square footage that was leased”).
-   **DOM Content Selector (Advanced)** (Optional): Specify the DOM selector containing the content to extract. By default, this uses “body.”
