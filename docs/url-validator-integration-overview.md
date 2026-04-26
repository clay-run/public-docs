---
title: URL Validator integration
source_url: https://university.clay.com/docs/url-validator-integration-overview
description: Check if a URL is active and reachable.
last_synced: 2026-04-26T01:40:51.282Z
upstream_hash: 58001c0d4d0ff77c3e74662185c86f3710e69ead192abbdc932e7940b343980e
---

# URL Validator integration

Check if a URL is active and reachable.

# Enrichment overview

The **Check if URL is Valid** action determines whether a given URL is active and reachable. It validates URLs by checking their response status and identifying any errors.

# Available actions

## `Action` Check if URL is Valid

### Overview

The **Check if URL is Valid** action determines whether a given URL is active and reachable. It validates URLs by checking their response status and identifying any errors.

-   A URL is considered **valid** if the site exists, is reachable, and does not return errors like a 404 (not found) status.
-   If the site returns errors (e.g., 404) or cannot be accessed, the URL is marked as **invalid**.

### Input fields

-   URL: URL of the link you want to verify.

### Output fields

-   Valid:  A boolean (true or false) indicating if the URL is valid.
