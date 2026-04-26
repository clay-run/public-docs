---
title: Yelp integration
source_url: https://university.clay.com/docs/yelp-integration-overview
description: Local business discovery platform with user reviews.
last_synced: 2026-04-26T01:40:57.488Z
upstream_hash: 15ff01e69ac7f6ebf28b20733b088a43f06783546f8f72f18a6d48dd624a7ad8
---

# Yelp integration

Local business discovery platform with user reviews.

## **Yelp Overview**

The Yelp integration in Clay allows users to access local business data, including details, reviews, and search results by location and category.

## **Available Actions with the Yelp Integration**

### **`Action` Search for a Candidate**

Use this action to search for businesses on Yelp based on location and a specific search query.

**Setup Inputs**

-   **Location**: Enter the location for the business search (e.g., “San Francisco, CA” or “94103”).
-   **Search Query** (Optional): Specify a search term, like “coffee shop.”
-   **Yelp Domain** (Optional): Set the Yelp domain to search (defaults to [yelp.com](http://yelp.com)).
-   **Sort Results By** (Optional): Choose how results are sorted (defaults to recommended).
-   **Limit** (Optional): Specify the number of results to return (max: 10, defaults to 5).
-   **Include Ad Results?** (Optional): Enable to include Yelp ad results in the response.

### **`Action` Find Reviews**

Use this action to retrieve reviews for a specific business identified by a Place ID.

**Setup Inputs**

-   **Place ID**: Provide the unique Yelp Place ID from a previous business search.
-   **Search Query** (Optional): Specify text to search within reviews (e.g., “great service”).
-   **Review Language** (Optional): Filter reviews by language.
-   **Yelp Domain** (Optional): Choose the Yelp domain to use (defaults to [yelp.com](http://yelp.com)).
-   **Sort Reviews By** (Optional): Set the sorting order for reviews (defaults to relevance).
-   **Limit** (Optional): Set the number of reviews to return (max: 10, defaults to 5).

### **`Action` Find Business Info**

Use this action to retrieve detailed information about a business using location and search criteria.

**Setup Inputs**

-   **Business Name**: Enter the exact business name (e.g., “Eric’s Coffee Roasters”).
-   **Location**: Specify the business location (e.g., “San Francisco, CA”).
-   **Yelp Domain** (Optional): Set the Yelp domain for the search (defaults to [yelp.com](http://yelp.com)).
