---
title: GitHub integration
source_url: https://university.clay.com/docs/github-integration-overview
description: Software development platform.
last_synced: 2026-04-26T01:40:02.107Z
upstream_hash: 8fedd484277976eb3eadd6ecf62b0515fb3ae6dce7a19eb5ff38189094ee0f89
---

# GitHub integration

Software development platform.

## Github Overview

The Github integration allows you to easily access and analyze GitHub data in Clay, including user details, repository metrics, contributors, stargazers, forks, and email addresses, as well as perform searches and retrieve repository lists for organizations.

## Setting up Github and Clay integration

To set up the Github integration, connect your Linear account by signing in via OAuth. You can access this in the **Settings > Connections** or via any integration panel.

## **Available Actions with the Github Integration**

### `Action` Find Email from Username or Search

Use this action to retrieve an email address associated with a GitHub user by username or search query using recent commit data.

**Setup Inputs**

-   **Username** (Optional): Enter or select a column containing the GitHub username (e.g., “eengoron”) to find the email.
-   **Search Query** (Optional): Provide a search query to refine results (e.g., “Eric Engoron” or “tom repos:>30”).

### `Action` Find User Details

Use this action to retrieve essential information about a GitHub user by username or profile URL.

**Setup Inputs**

-   **Username**: Enter or select a column containing the GitHub username to retrieve user details.
-   **Include Repos** (Optional): Select to include information about the user’s repositories.
-   **Include Orgs** (Optional): Select to include information about the user’s organizations.
-   **Include Contributions** (Optional): Select to include the number of user contributions over the past year.
-   **Include Starred** (Optional): Select to include the number of repositories the user has starred.

### `Action` Find Repo Summary

Use this action to retrieve key metrics for a specified GitHub repository.

**Setup Inputs**

-   **Repository URL**: Enter or select a column containing the URL of the GitHub repository to get metrics.

Github Overview
