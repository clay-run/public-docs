---
title: ActiveCampaign integration
source_url: https://university.clay.com/docs/activecampaign-integration
last_synced: 2026-04-26T01:39:38.952Z
upstream_hash: 7dbc1e903d0b1a28abaee39a5599d189478a30aa99268f60bb8b7cc7ecc40742
---

# ActiveCampaign integration

Create and update info in ActiveCampaign.

ActiveCampaign is a customer experience automation platform that combines email marketing, marketing automation, and CRM capabilities.

Using this integration, you can look up, create, and update information in ActiveCampaign directly within your Clay table.

## **Enriching data with ActiveCampaign**

1.  While in a Clay table, click `Add enrichment` and search for `ActiveCampaign`.
2.  Under `Integrations`, select one of the ActiveCampaign options.
3.  In the modal, you will be asked to `Select ActiveCampaign account`.
    -   If you haven't already connected your ActiveCampaign account, click `+ Add account` and go through authentication.

### **`Action` Create object**

Creates a new object in your ActiveCampaign.

**Inputs**:

-   **Object type**: Account or Contact
-   **For `Account`**:
    -   **Company name**
    -   **Website (Optional)**
    -   **Owner (Optional)**
    -   **Description (Optional)**
    -   **Address (Optional)**
    -   **Number of Employees (Optional)**
    -   **Annual Revenue (Optional)**
    -   **Industry/Vertical (Optional)**
    -   **Phone Number (Optional)**
-   **For `Contact`**:
    -   **Email**
    -   **First Name (Optional)**
    -   **Last Name (Optional)**
    -   **Phone Number (Optional)**

### **`Action` Update object**

Updates an existing object in ActiveCampaign.

**Inputs**:

-   **Object type**: Account or Contact
-   **Object ID**: ID of the object you want to update.
-   **For `Account`**:
    -   **Company name**
    -   **Website (Optional)**
    -   **Owner (Optional)**
    -   **Description (Optional)**
    -   **Address (Optional)**
    -   **Number of Employees (Optional)**
    -   **Annual Revenue (Optional)**
    -   **Industry/Vertical (Optional)**
    -   **Phone Number (Optional)**
-   **For `Contact`**:
    -   **Email**
    -   **First Name (Optional)**
    -   **Last Name (Optional)**
    -   **Phone Number (Optional)**

### **`Action` Lookup object**

Finds an object in ActiveCampaign.

**Inputs**:

-   **Object Type**: Account or Contact
-   **Filter Type**: ActiveCampaign ID or Email

### **`Action` Create an association**

Links a contact to an account in ActiveCampaign.

**Inputs**:

-   **Contact ID**
-   **Account ID**
-   **Job Title (Optional)**

### **`Action` Add to automation**

Adds a contact to an automation workflow in ActiveCampaign.

**Inputs**:

-   **Contact ID**
-   **Automation ID**

### **Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))
