---
title: HeyReach integration
source_url: https://university.clay.com/docs/heyreach-integration-overview
description: LinkedIn automation software.
last_synced: 2026-04-26T01:40:07.367Z
upstream_hash: 3eda48c3b7abff7daa02660f5d9bc37689f78cdd43e5a7e70b2e942d01dccda0
---

# HeyReach integration

LinkedIn automation software.

HeyReach is an automation platform that helps sales teams and agencies automate multi-sender outreach campaigns at scale. Within Clay, you can use HeyReach to add leads directly to your campaigns and map personalization variables for custom sequences.

## Enriching data with HeyReach

1.  While in a Clay table, click `Add enrichment` and search for `HeyReach`.
2.  Under `Integrations`, select one of the HeyReach actions.
3.  In the modal, you will be asked to `Select HeyReach account`.
    -   If you haven't already connected your HeyReach account, click `+ Add account` and enter your API key. You can find your API key by going to `Integrations` > `HeyReach API` in your HeyReach account.

**Note:** Before running this action, you must create an active campaign in HeyReach. Campaigns cannot be created from within Clay.

### `Action` Add Lead to Campaign

Use this action to add a lead to an existing HeyReach campaign from a professional profile URL.

**Inputs**

Required:

-   **Campaign ID:** The HeyReach campaign you want to add the lead to. Displays as a dropdown populated from your HeyReach account.
-   **First name:** The first name of the lead.
-   **Last name:** The last name of the lead.
-   **Professional URL:** The profile URL of the lead (e.g., `https://linkedin.com/in/examplename`).

Optional:

-   **LinkedIn account:** The LinkedIn sender account you want to use for the campaign. If left empty, leads will be automatically assigned to any active LinkedIn sender in the campaign.
-   **Location:** The lead's location (e.g., `London`).
-   **Company name:** The company where the lead is employed.
-   **Current position:** The lead's current job title.
-   **Email address:** The lead's email address.
-   **Summary:** A brief summary of the lead.
-   **About:** Additional information about the lead. Supports formula mode.
-   **Custom fields:** Key-value pairs for personalization variables used in your HeyReach sequences. Custom field names must exactly match the variable names you defined in HeyReach and can only contain alphanumeric characters and underscores (e.g., `my_custom_field`).

**Outputs**

-   **Added Leads Count:** The number of leads successfully added to the campaign.
-   **Updated Leads Count:** The number of existing leads updated in the campaign.
-   **Failed Leads Count:** The number of leads that failed to be added.

### Run settings

-   **Auto-update:** Recommended for trigger-based campaigns so that new rows added to Clay are automatically pushed to HeyReach.
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

## Troubleshooting

### Custom field values aren't being personalized in my sequences

Custom field names in Clay must be an exact match to the variable names in your HeyReach sequence (e.g., a Clay custom field named `AI_icebreaker` will only populate a HeyReach variable also named `AI_icebreaker`). Spaces in field names are automatically converted to underscores. Only alphanumeric characters and underscores are supported.

### My campaign shows "Finished" status in HeyReach

This is expected behavior for a newly created campaign. Once Clay adds the first lead, the campaign status will update to "Ongoing."

### Leads are not being added to the campaign

Ensure your HeyReach campaign was created with `Create empty list` and is designated as a lead list. The campaign must be Active for leads to be added successfully.
