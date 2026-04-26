---
title: Sendspark integration
source_url: https://university.clay.com/docs/sendspark-integration-overview
last_synced: 2026-04-26T01:40:39.562Z
upstream_hash: e31c1a1697b958c6f5d379c0525bf06381e39dd5cc52dba078aa818b8d1f0d2f
---

# Sendspark integration

AI-powered video creation platform boosting sales and marketing outreach via personalized videos.

The Sendspark integration enables you to effortlessly create AI-personalized videos for prospects within your sales automations.

With this integration, you can automatically add prospects to video campaigns and generate personalized dynamic videos based on the selected campaign.

## **Enriching data with Sendspark**

1.  While in a Clay table, click `Add enrichment` and search for `Sendspark`.
2.  Under `Integrations`, select one of the Sendspark options.
3.  In the modal, you will be asked to `Select Sendspark account`.
    -   If you haven't already connected your Sendspark account, click `+ Add account` and go through authentication.

### `Action` Add Prospect to Video Campaign

Use this action to automatically add a prospect from Clay to a Sendspark video campaign, generating a personalized dynamic video based on the selected campaign.

**Inputs**

-   **Workspace ID**: Enter the ID of your Sendspark workspace.
-   **Dynamic Campaign ID**: Enter the ID of the dynamic campaign to which you want to add the prospect.
-   **Contact Name**: Provide the name of the prospect.
-   **Contact Email**: Provide the prospect's email address.
-   **Company Name** (Optional): Enter the name of the prospect's company.
-   **Job Title** (Optional): Enter the job title of the prospect.
-   **Background URL**: Provide a URL for a background image in the video.
-   **Allow Duplicate Prospects** (Optional): Set to "true" to add a new prospect even if one with the same email already exists.

### **Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))
