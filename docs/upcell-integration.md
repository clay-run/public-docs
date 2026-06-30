---
title: Upcell integration
description: Find mobile numbers from LinkedIn profiles.
last_synced: 2026-04-26T01:40:50.636Z
---

# Upcell integration

Find mobile numbers from LinkedIn profiles.

Upcell is a mobile number lookup tool for finding contact information from LinkedIn profiles.

With this integration, you can find mobile numbers associated with LinkedIn profiles directly in Clay.

## **Enriching data with Upcell**

1.  While in a Clay table, click `Add enrichment` and search for `Upcell`.
2.  Under `Integrations`, select one of the Upcell options.
3.  In the modal, you will be asked to `Select Upcell account`.
    -   If you have your own account, click `+ Add account` and go through authentication. Otherwise, use the Clay provided key.

### `Action` Find mobile number

Find person's mobile number from their professional social profile.

**Inputs:**

-   **Professional profile URL:** The profile URL of the person whose phone number you want to look up. This input requires a column with the **Personal profile URL** data type — not a plain text column that happens to contain a profile URL string. Columns with this type are created automatically by Clay's people-search imports, Enrich Person, and similar enrichments that return professional profile URLs.

### **Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

## Troubleshooting

### "Missing profile URL" error despite having a profile URL

If Upcell reports a missing profile URL error when a row appears to have a professional profile URL, confirm that the **Professional profile URL** input is mapped to a column with the **Personal profile URL** data type.

Columns with this data type are created automatically by Clay's Find People imports, Enrich Person, Find Personal Profile, and other enrichments that return professional profile URLs. The input selector in the Upcell configuration shows only compatible columns by default.

If your profile URL is in a plain text column, use the profile URL column from a Find People import or run an Enrich Person step to get a properly typed column, then map that column to the **Professional profile URL** input.
