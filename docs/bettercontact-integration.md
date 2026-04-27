---
title: BetterContact integration
source_url: https://university.clay.com/docs/bettercontact-integration
description: Find work emails and mobile phones.
last_synced: 2026-04-27T18:09:22.050Z
upstream_hash: ed2f965be94a1937199a9bea1b230d7ec8368ddb1f732e26c3f1912cb65084b0
---

# BetterContact integration

Find work emails and mobile phones.

BetterContact is a contact enrichment tool for finding verified work emails and mobile phone numbers.

With this integration, you can automatically find and verify contact information for your prospects, including work email addresses and mobile phone numbers.

## Setting up the BetterContact integration

1.  While in a Clay table, click `Add enrichment` and search for BetterContact.
2.  Under `Integrations`, select one of the BetterContact options.
3.  In the modal, you will be asked to `Select BetterContact account`.
    1.  If you have your own account, click `+ Add account` and go through authentication. Otherwise, use the Clay provided key.

## Using the BetterContact integration

### `Action` Find work email

Use this action to find a person's work email from name and company domain or company name.

_Note: If you have a BetterContact pro plan, they will charge you for safe catch-all emails but not unsafe catch-all emails. Otherwise, BetterContact will charge you for all catch-all emails._

**Inputs**

-   **Person’s name**
-   **Company name (Optional)**
-   **Company domain (Optional)**
-   **Social URL (Optional):** Select a column with a social media URL.
    -   _Providing the person's social URL may increase accuracy._

**Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

### `Action` Find mobile phone

Find a person's mobile phone from name and company domain or company name.

**Inputs**

-   **Person’s name**
-   **Company name (Optional)**
-   **Company domain (Optional)**
-   **Social URL (Optional):** Select a column with a social media URL.
    -   _Providing the person's social URL may increase accuracy._

**Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))
