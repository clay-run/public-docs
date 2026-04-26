---
title: Lob integration overview
source_url: https://university.clay.com/docs/lob-integration-overview
description: Automated direct mail marketing platform
last_synced: 2026-04-26T01:40:16.885Z
upstream_hash: d04aee7f496ae69b7b165e84529eb667fac3be58f6ac0bcd297d358218210710
---

# Lob integration overview

Automated direct mail marketing platform

## Lob Overview

The Lob integration allows you to retrieve information about products on a Lob-hosted website and check the hosting status of any store. This integration is useful for identifying if a website is hosted on Lob and accessing product details directly from the store.

## Setting up Lob and Clay integration

To set up the Lob integration, connect your Lob account by adding your API key. You can access this in the **Settings > Connections** or via any integration panel.

For more help, vsit Lob’s [documentation](https://help.lob.com/account-management/api-keys) on where to find your API key.

## **Available Actions with the Lob Integration**

### `Action` Validate International Address

Use this action to validate and format an international address within Clay workflows using Lob’s International Address Verification API.

**Setup Inputs**

-   **Full Address**: Enter or select a column containing the full international address to validate.

### `Action` Validate U.S Address

This action verifies if a given site is hosted on Lob, helping you confirm platform compatibility.

Use this action to validate and format a U.S. address within Clay workflows using Lob’s Address Verification API.

**Setup Inputs**

-   **Full Address**: Enter or select a column containing the full U.S. address to validate, e.g., “123 Main St, San Francisco, CA 94105.”
