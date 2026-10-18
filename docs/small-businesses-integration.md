---
title: Small businesses integration
description: Find local businesses and read their reviews from an online business directory using location and search queries directly in Clay tables.
last_synced: 2026-07-21T04:45:09.986Z
---

# Small businesses integration

Local business discovery platform with user reviews.

The Small Businesses integration lets you find local businesses and read their reviews using a location and a search query. Use it to source businesses from an online business directory, pull key details (ratings, review counts, contact info, and more), and retrieve individual reviews — all directly in your Clay tables.

**Note:** These actions don't require an API key — they're ready to use as soon as you add them to a table.

## Add the Small Businesses actions

1.  In a Clay table, click `Actions` and search for `Small Businesses`.
2.  Select the action you want: `Find small businesses`, `Find small business information`, or `Find small business reviews`.
3.  Map your input columns and run.

## Available actions

### `Action` Find small businesses

Find small businesses in a business directory using a location and search query.

**Inputs**

-   `Location` **(Required)** — The location to search. A variety of formats are accepted: a full address, city and state, city, or ZIP code (e.g., `706 Mission St, San Francisco, CA`, `San Francisco, CA`, `94103`).
-   `Search Query` **(Optional)** — A search term, e.g., `Coffee Shop`.
-   `Directory domain` **(Optional)** — The business directory domain to search. Defaults to `yelp.com`.
-   `Sort Results By` **(Optional)** — `Recommended` (default), `Highest Rated`, or `Most Reviewed`.
-   `Limit` **(Optional)** — The number of results to return (max: 10, defaults to 5).
-   `Include Ad Results?` **(Optional)** — Turn on to include ad results in the response.

**Outputs**

-   `Businesses` — A list of matching businesses. Each includes `Position`, `Place Ids`, `Title`, `Link`, `Reviews Link`, `Categories`, `Price`, `Rating`, `Reviews`, `Neighborhoods`, `Phone`, `Snippet`, `Thumbnail`, and `Button`.
-   `Directory Search Link` — The directory search URL for your query.

**Pricing:** 1 credit per row.

### `Action` Find small business information

Given a business name and location, find detailed information about a small business from its business-directory page.

**Inputs**

-   `Business Name` **(Required)** — The exact business name, e.g., `Eric's Coffee Roasters`.
-   `Location` **(Required)** — The business location (same formats as above).
-   `Directory domain` **(Optional)** — The business directory domain to search. Defaults to `yelp.com`.

**Outputs**

-   `Place Ids`, `Title`, `Link`, `Rating`, `Reviews`, `Highlights`, `Snippet`, `Response Time`, `Service Requests`, `Thumbnail`, `First Review` (date, rating, text), and `Last Review` (date, rating, text).

**Pricing:** 2 credits per row.

### `Action` Find small business reviews

Find reviews for a small business using a `Place ID` from a `Find small businesses` search.

**Inputs**

-   `Place ID` **(Required)** — The business's Place ID. Take this from a `Find small businesses` result.
-   `Search Query` **(Optional)** — Search for text within reviews, e.g., `great service`.
-   `Review Language` **(Optional)** — Filter reviews by a specific language.
-   `Directory domain` **(Optional)** — The business directory domain to use. Defaults to `yelp.com`.
-   `Sort Reviews By` **(Optional)** — `Relevance` (default), `Newest First`, `Oldest First`, `Highest Rated`, `Lowest Rated`, or `Elite Users Only`.
-   `Limit` **(Optional)** — The number of reviews to return (max: 10, defaults to 5).

**Outputs**

-   `Business Name`, `Total Number Of Reviews`, and `Reviews Url`.
-   `Reviews` — A list of reviews. Each includes the reviewer (`User`), the review `Comment`, `Date`, `Rating`, any `Owner Replies`, `Photos`, and `Feedback` (useful, funny, and cool counts).

**Pricing:** 1 credit per row.
