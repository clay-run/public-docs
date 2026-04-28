---
title: HubSpot integration
source_url: https://university.clay.com/docs/hubspot-integration-overview
description: All-in-one CRM platform for marketing, sales, and customer service.
last_synced: 2026-04-26T01:40:09.362Z
upstream_hash: 59e6ef2464cbe62bf1c3eccafec2aa4eb3962fbd661770629a2ff87a6429f2e3
---

# HubSpot integration

All-in-one CRM platform for marketing, sales, and customer service.

HubSpot is a customer relationship management (CRM) platform that helps businesses manage sales, marketing, and customer service.

With this integration, you can import, create, update, and manage HubSpot objects directly in Clay.

## Enriching data with HubSpot

1.  While in a Clay table, click `Add enrichment` and search for `HubSpot`.
2.  Under `Integrations`, select one of the HubSpot options.
3.  In the modal, select your HubSpot account.
    -   If you haven't connected your HubSpot account yet, click `+ Add account` and complete authentication.

### `Source` Import objects from HubSpot

Use this source to import objects from HubSpot into Clay.

**Inputs**

-   **Object type:** The type of HubSpot object to import.
-   **List to pull objects from (Optional):** Select a list to pull objects from. If no list is selected, all objects will be pulled.
-   **Include read-only properties? (Optional):** Include all HubSpot calculated fields for each contact (e.g., `hs_analytics_first_timestamp`). If not selected, only editable properties will be included (e.g., `domain`).
-   **Exclude empty properties? (Optional):** Exclude all empty properties from the response. If not selected, all properties will be included, even those with empty values.

**Note:** The source import is additive. If you later update the HubSpot list's filters so that some records are excluded, those records stay in your Clay table — Clay does not automatically remove existing rows when list membership changes. To get a fresh import that exactly matches the current list, delete and re-run the source. See [Sources FAQs](https://university.clay.com/docs/sources#faqs) for more detail.

### `Action` Create object

Use this action to create an object in HubSpot.

**Inputs**

-   **Object type:** The type of HubSpot object to create.

### `Action` Lookup object

Use this action to look up an object in HubSpot.

**Inputs**

-   **Object type:** The type of HubSpot object to look up.
-   **Remove blank values from results (Optional):** Helpful for reducing result size.
-   **Limit (Optional):** Maximum number of objects to return. Defaults to 10.

### `Action` Update object

Use this action to update an object in HubSpot.

**Inputs**

-   **Object type:** The type of HubSpot object to update.
-   **HubSpot Object ID:** The unique identifier of the object to update.

### `Action` Create association

Use this action to create an association between two objects in HubSpot.

**Inputs**

-   **From object type:** The type of the source object.
-   **To object type:** The type of the target object.
-   **Association type:** The type of association to create.
-   **From Object ID:** The ID of the source object.
-   **To Object ID:** The ID of the target object.

### `Action` Retrieve associated objects

Use this action to retrieve associations between two objects in HubSpot.

**Inputs**

-   **From object type:** The type of the source object.
-   **To object type:** The type of the target object.
-   **From object ID:** The unique identifier of the object you want to look up associations for.
-   **Remove blank values from results (Optional):** Exclude empty properties from the response.
-   **Include read-only properties (Optional):** Include calculated fields in the response.
-   **Limit (Optional):** Maximum number of objects to return. Defaults to 20.

### `Action` Find owner

Use this action to find a HubSpot owner by ID or email address.

**Inputs**

-   **Owner ID (Optional):** The HubSpot owner ID to search for. If both ID and email are provided, the email will be validated against the owner found by ID.
-   **Email (Optional):** The email address to search for. If both ID and email are provided, the email will be validated against the owner found by ID.

## OAuth scopes

When connecting your HubSpot account, Clay uses optional OAuth scopes to give you fine-grained control over permissions.

Learn more about [optional scopes](https://university.clay.com/docs/oauth-optional-scopes).

### Required scopes

These permissions cannot be disabled and are always requested:

-   [`crm.lists.read`](http://crm.lists.read) — View contact list details.
-   [`crm.objects.contacts.read`](http://crm.objects.contacts.read) — View contact properties and details.
-   [`crm.objects.companies.read`](http://crm.objects.companies.read) — View company properties and details.
-   [`crm.objects.leads.read`](http://crm.objects.leads.read) — View lead properties and details.
-   [`crm.objects.owners.read`](http://crm.objects.owners.read) — View details about users assigned to CRM records.
-   [`crm.schemas.companies.read`](http://crm.schemas.companies.read) — View company property settings.
-   [`crm.schemas.contacts.read`](http://crm.schemas.contacts.read) — View contact property settings.

### Optional scopes (enabled by default)

These permissions are requested by default but can be disabled:

-   `crm.objects.companies.write` — Create, delete, or edit companies.
-   `crm.objects.contacts.write` — Create, delete, or edit contacts.
-   `crm.objects.leads.write` — Create, delete, or edit leads.
-   [`crm.schemas.custom.read`](http://crm.schemas.custom.read) — View custom object definitions.
-   [`crm.objects.custom.read`](http://crm.objects.custom.read) — View custom objects.
-   `crm.objects.custom.write` — Create, delete, or edit custom objects.
-   [`crm.objects.deals.read`](http://crm.objects.deals.read) — View deal properties and details.
-   \[`crm.objects.deals](<http://crm.objects.deals>).write` — Create, delete, or edit deals.
-   [`crm.schemas.deals.read`](http://crm.schemas.deals.read) — View deal property settings.

### Optional scopes (disabled by default)

These permissions are available but not requested by default:

-   [`automation.sequences.read`](http://automation.sequences.read) — View sequence details.
-   `automation.sequences.enrollments.write` — Enroll contacts in a sequence.

### Run settings

-   **Auto-update**
-   **Only run if:** The enrichment will only run when conditions are met. [Learn more about conditional formulas](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101).
