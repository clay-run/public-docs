---
title: Groove integration
source_url: https://university.clay.com/docs/groove-integration
last_synced: 2026-04-26T01:40:05.747Z
upstream_hash: f9006a1fd0ad68510d742f4479228779ab08930e9aca93e7a9384ef3fa34e866
---

# Groove integration

Automate workflows with your Groove account.

Groove is a platform for customer support and help desk management.

With this integration, you can automate workflows between Clay and your Groove help desk.

## Setting up the Groove integration

1.  While in a Clay table, click `Add enrichment` and search for Groove.
2.  Under `Integrations`, select one of the Groove options.
3.  In the modal, you will be asked to `Select Groove account`.
    1.  If you haven’t already connected, click `+ Add account` and go through authentication.

## Using the Groove integration

### `Action` List flows

Use this action to list flows in your Groove account.

**Inputs**

-   **Filter type:** Choose to filter by Active flows or not.
-   **Owner ID filter (Optional):** Filter for flows owned by a specified user.

**Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

### `Action` List people

Use this action to list people in your Groove account.

**Inputs**

-   **Filter type:** Choose to filter by people who are involved in specific flows.
-   **Flow ID filter (Optional):** Enter the flow ID you want to filter by.

**Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

### `Action` List users

Use this action to list users in your Groove account.

**Inputs**

-   **Filter type:** Choose to filter by email, SFDC ID, or none.
-   **Flow ID filter (Optional):** Enter the email or SFDC ID of the specific user to find.

**Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

### `Action` Add person to flow

Add a person to a flow in your Groove account.

**Inputs**

-   **Flow ID**
-   **Person SDFC ID**
-   **Owner ID (Optional):** The Groove user ID that should own the person imported into the flow.

**Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

### `Action` Assign a user an action

Assign a user an action in your groove account.

**Inputs**

-   **Filter input fields: Search fields by name or description**
-   **Assignee:** Groove user ID.
-   **Action type**
-   **Summary:** Title of this action.
-   **Due by time**
-   **Priority (Optional)**
-   **Description (Optional)**
-   **Body (Optional)**
-   **Logging: Salesforce task type (Optional)**
-   **Logging: Salesforce Lead or Contact (Optional):** A comma-separated list of SFDC Lead or Contact IDs.
-   **Logging: Salesforce Object (Optional):** A comma-separated list of SFDC "ObjectType:ID" pairs to log this action to.

**Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))
