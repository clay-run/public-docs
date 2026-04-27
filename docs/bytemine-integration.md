---
title: Bytemine integration
source_url: https://university.clay.com/docs/bytemine-integration
description: Enrich person data to gain deeper insights for outreach and
  relationship-building efforts
last_synced: 2026-04-27T18:09:29.052Z
upstream_hash: 3268cb8b68b632a4b5c6930be170a74e46d0875a201b65b21111a4f679a882e9
---

# Bytemine integration

Enrich person data to gain deeper insights for outreach and relationship-building efforts

Bytemine enhances contact profiles by compiling detailed personal and professional information using minimal input data.

With this integration, you can enrich person data to gain deeper insights for outreach and relationship-building efforts.

## **Enriching data with Bytemine**

1.  While in a Clay table, click `Add enrichment` and search for `Bytemine`.
2.  Under `Integrations`, select one of the Bytemine options.

### `Action` Enrich Person

Use this action to retrieve deeper contact and profile data for individuals by leveraging limited available information.

**Inputs**

-   **Email address:** Work or personal email of the person
-   **Professional profile URL:** LinkedIn profile URL (e.g., `https://www.linkedin.com/in/john-doe`)
-   **Facebook profile URL:** Facebook profile URL
-   **Person's name:** Full name of the person
-   **Require work email:** Only return results if a work email is present
-   **Require personal email:** Only return results if a personal email is present
-   **Require direct dial:** Only return results if a direct dial phone number is present
-   **Require mobile phone:** Only return results if a mobile phone number is present

**Output**

-   Contact information (email addresses, phone numbers)
-   Professional details (current role, work experience)
-   Personal information (age, gender, location)
-   Company information (size, revenue, industry)

### **Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))
