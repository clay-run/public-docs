---
title: Loxo integration
source_url: https://university.clay.com/docs/loxo-integration-overview
last_synced: 2026-04-26T01:40:18.188Z
upstream_hash: 2c43b1990d09508c96da443bdca21bd6456dc1e63ff4e3419362c90f0f3b2f86
---

# Loxo integration

Talent intelligence platform streamlining recruitment.

Loxo is an AI-powered talent intelligence platform that combines ATS, CRM, and recruitment tools to streamline recruiting workflows. Within Clay, you can pull candidate records directly from Loxo lists, find and create people, update existing profiles, and retrieve activity history.

## **Creating a table with Loxo**

1.  While in a workbook, click `+ Add` and select `Source`.
2.  Search for `Loxo` and select it.
3.  In the modal, you will be asked to select a Loxo account.
    -   If you haven't connected your account yet, click `+ Add account` and enter your **Agency Slug** (as the username) and **API Key** (as the password). You can find both in Loxo's [developer documentation](https://loxo.co/).

### **`Source`** **Pull in People from Lists in Loxo**

Imports all people from one or more of your Loxo lists into Clay as rows.

**Inputs**

-   **List(s) to Pull From**: The Loxo list(s) you want to import people from. Displays as a multi-select dropdown populated from your connected Loxo account.

_Note: This source pulls a maximum of 10,000 people per run._

## **Enriching data with Loxo**

1.  While in a Clay table, click `Add enrichment` and search for `Loxo`.
2.  Under `Integrations`, select one of the Loxo actions.
3.  In the modal, you will be asked to select a Loxo account.
    -   If you haven't connected your account yet, click `+ Add account` and enter your **Agency Slug** (as the username) and **API Key** (as the password). You can find both in Loxo's [developer documentation](https://loxo.co/).

### **`Action`** **Find Person**

Finds a person in your Loxo account using an email address, professional social URL, or Loxo ID.

**Inputs**

-   **Email Address, Professional Social URL, or Loxo ID**: The unique identifier of the person you want to find

**Outputs**

-   **Total People Found**: The total number of matching records found in Loxo
-   **Person**: The matched person record, including name, email addresses, professional social URL, phone number, current job title, current company, description, personal website, Loxo ID, and owner name

### **`Action`** **Create Person**

Creates a new person record in your Loxo account.

**Inputs**

-   **Name**: The full name of the person to create
-   Description (Optional): Notes or a brief description about the person
-   Email Address (Optional): The person's email address
-   Professional Social URL (Optional): The person's professional social profile URL
-   Phone Number (Optional): The person's phone number
-   Personal Website (Optional): The URL of the person's personal website
-   Current Job Title (Optional): The person's current job title
-   Current Company Name (Optional): The name of the person's current employer
-   Person Owner ID (Optional): The Loxo user to assign as the owner of this record. Displays as a dropdown populated from your Loxo account
-   Tags (Optional): A comma-separated list of tags to apply to the person
-   Add to List(s) (Optional): One or more Loxo lists to add this person to. Displays as a multi-select dropdown
-   Custom Fields (Optional): Any custom person fields configured in your Loxo account

**Outputs**

-   **Person**: The newly created person record, including all submitted fields and the assigned Loxo ID
-   **Loxo URL**: A direct link to the person's profile in Loxo

### **`Action`** **Update Person**

Updates an existing person record in your Loxo account.

**Inputs**

-   **Person ID**: The Loxo ID of the person to update. Typically retrieved from a prior **Find Person** action or from a Loxo source
-   Name (Optional): The updated name of the person
-   Description (Optional): Updated notes or description
-   Email Address (Optional): The updated email address
-   Professional Social URL (Optional): The updated professional social profile URL
-   Phone Number (Optional): The updated phone number
-   Personal Website (Optional): The updated personal website URL
-   Current Job Title (Optional): The updated job title
-   Current Company Name (Optional): The updated company name
-   Person Owner ID (Optional): The updated owner of the record. Displays as a dropdown
-   Tags (Optional): A comma-separated list of tags to add. Note: This will not remove existing tags
-   Add to List(s) (Optional): One or more lists to add the person to. Note: This will not remove existing list memberships
-   Custom Fields (Optional): Any custom person fields configured in your Loxo account

**Outputs**

-   **Person**: The updated person record
-   **Loxo URL**: A direct link to the updated person's profile in Loxo

### **`Action`** **Find Activity**

Retrieves activity records of a specific type associated with a person in your Loxo account.

**Inputs**

-   **Person ID**: The Loxo ID of the person whose activity you want to retrieve. Typically sourced from a prior **Find Person** action
-   **Activity Type**: The type of activity to retrieve (e.g., notes, emails, tasks). Displays as a dropdown populated from your Loxo account

**Outputs**

-   **Person Events**: A list of activity records matching the selected type, including activity details, creation date, and the name of the user who created each activity

### Run settings

-   `Auto-update`
-   `Only run if:` The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))
