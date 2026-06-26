---
title: People Data Labs integration overview
description: Enrich B2B person and company profiles with comprehensive, actionable data.
last_synced: 2026-04-26T01:40:27.701Z
---

# People Data Labs integration overview

Enrich B2B person and company profiles with comprehensive, actionable data.

## **Getting started with People Data Labs**

The People Data Labs integration in Clay enables users to enrich person data, find personal emails, and generate segmented lists of people based on query parameters in Clay.

With People Data Labs, you can perform a variety of actions, including:

-   Enrich Company
-   Enrich Person
-   Find Personal Email
-   Get Employee Count by Criteria

With People Data Labs, you can perform a variety of actions, including:

## **Getting better email and phone number coverage with waterfall enrichments**

People Data Labs is great for finding email and phone number contacts, but it's not the only way to get this data.

For better coverage on email data, we recommend using [Clay's waterfall enrichments](https://www.clay.com/waterfall-enrichment), which will let you search sequentially across multiple data providers. Learn more on how to use Clay waterfalls with this [Clay University lesson](https://www.clay.com/university/lesson/enrich-people-waterfalls-clay-101).

With that in mind, let's dive into using People Data Labs within Clay!

## **Connecting with Clay with People Data Labs**

### **Option 1: Use the Clay-managed People Data Labs account**

By default, People Data Labs enrichments will use the Clay-managed People Data Labs account. This means that any new enrichment will charge the designated credit amount.

Simply pull up any People Data Labs enrichment within Clay to use the Clay-managed People Data Labs account.

For more information on how many credits you'll be charged for each action, check out the list below.

### **Option 2: Add your own People Data Labs API key**

If you are currently on a paid plan, you can use your own People Data Labs account within Clay through an API key.

You can access your People Data Labs API key through the **Integrations** section.

You can add your API key by **Add Account** through any People Data Labs enrichment.

## Available actions with the People Data Labs integration

### `Action` Enrich Company

Retrieve enriched company data such as industry, revenue, employee count, and more.

**Setup Inputs**

-   **Company Domain**: The company's primary domain, e.g., [google.com](http://google.com).
-   **Company Social Profile** (Optional): Social URL for the company, e.g., LinkedIn profile.
-   **Company Stock Ticker** (Optional): Stock ticker symbol like "GOOGL."
-   **Minimum Likelihood Score** (Optional): Set a likelihood score threshold to refine data accuracy.

**Parent and subsidiary company data**

The Enrich Company result includes an **Affiliated Entities** array. Each entry in this array contains:

-   **Affiliated ID**: The PDL ID of the affiliated company.
-   **Display Name**: The company name (e.g., "Alphabet Inc.").
-   **Employee Count**: The number of employees at the affiliated company.
-   **Relationship**: The type of relationship — `ultimate_parent` or `immediate_parent`.

To enrich a company's ultimate parent with normalized details (name, website, industry, etc.), use a two-step approach:

1. Add a formula column that filters the **Affiliated Entities** array where **Relationship** equals `ultimate_parent` and extracts the **Display Name**.
2. Use that parent company name as the input for a second **Enrich Company** column — or a **Find Company Domain** enrichment — to retrieve the full normalized profile.

This means you don't need to do a separate lookup using a raw PDL parent ID. The parent company's display name is already available in the Affiliated Entities output from your initial enrichment.

### `Action` Enrich Person

Use this action to retrieve comprehensive personal data such as social profiles, contact details, and employment history using People Data Labs.

**Setup Inputs**

-   **Person's Name**: Provide the full name of the individual.
-   **Company Name**: Specify the company name associated with the person. Must be used with Person's Name.
-   **Social Media Profile URL** (Optional): Enter the LinkedIn or Facebook URL for the person to narrow down results.

### `Action` Find Personal Email

Retrieve a person's personal email by searching with available identifiers.

**Setup Inputs**

-   **Person's Name**: The individual's full name. Used in combination with Company Name.
-   **Company Name**: The company associated with the individual. Must be used with Person's Name.
-   **Social Media Profile URL** (Optional): Provide a LinkedIn or other social profile URL to improve accuracy.

### `Action` Get Employee Count by Criteria

Retrieve the employee count for a company based on role or geographic location criteria.

**Setup Inputs**

-   **Company Domain**: The domain URL of the company (e.g., [google.com](http://google.com)).
-   **Company Social Profile** (Optional): LinkedIn or other social media URL of the company.
-   **Company Stock Ticker** (Optional): Stock ticker symbol, such as "GOOGL."
-   **Role Filter** (Optional): Specify the job roles to filter the employee count.
-   **Country Filter** (Optional): Filter results by country for location-specific data.
