---
title: URL Validator integration
description: Check if a URL is active and reachable.
last_synced: 2026-04-26T01:40:51.282Z
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

-   URL: URL of the link you want to verify. You can enter a full URL (for example, `https://clay.com`) or just a domain (for example, `clay.com`).
-   Try variants (optional, off by default): If the original URL is invalid, the Check if URL is Valid action also tries other protocol and www. versions of the URL to find a valid one. For example, for `example.com` it tries `http://example.com`, `https://example.com`, and `www.example.com`.

### Output fields

-   Valid:  A boolean (true or false) indicating if the URL is valid.
-   Valid Url: The version of the URL that was found to be valid. This is useful when **Try variants** is on, because it shows which version (for example, the www. version) worked.

### Domains that only load with www.

Some companies' websites only load on the www. version of their domain (for example, `www.example.com` loads but `example.com` doesn't). If you check a bare domain with **Try variants** turned off, the Check if URL is Valid action only checks the `https://` version of exactly what you entered, so a domain like this can be marked invalid even though the company's website is live. Before you replace a domain that was marked invalid, turn on **Try variants** and run the Check if URL is Valid action again.
