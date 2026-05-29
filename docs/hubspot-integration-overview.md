---
title: HubSpot integration
source_url: https://university.clay.com/docs/hubspot-integration-overview
description: All-in-one CRM platform for marketing, sales, and customer service.
last_synced: 2026-04-26T01:40:09.362Z
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
-   **HubSpot Object ID:** The unique identifier of the object to update. This field does not auto-populate — you must manually select the column containing your HubSpot Record IDs. Click the field and type `/` to open the column picker, then select the appropriate column.
-   **Ignore blank values (Optional):** When enabled (default), blank values from Clay will be ignored in HubSpot — existing HubSpot values are left unchanged. When disabled, blank values from Clay will overwrite existing HubSpot field values.

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

## FAQs

### Why does lifecycle stage (or another dropdown field) show an internal code like `marketingqualifiedlead` instead of a readable label?

This is a known limitation of HubSpot's API: it returns the internal value for enum/dropdown properties rather than the display label you see in HubSpot's UI. For example, the lifecycle stage field returns `marketingqualifiedlead` instead of "Marketing Qualified Lead." Clay passes these values through as-is.

**Workaround:** Add a Formula column that maps the internal codes to readable labels. For the default HubSpot lifecycle stages, the mapping is:

| Internal value | Display label |
|---|---|
| `subscriber` | Subscriber |
| `lead` | Lead |
| `marketingqualifiedlead` | Marketing Qualified Lead |
| `salesqualifiedlead` | Sales Qualified Lead |
| `opportunity` | Opportunity |
| `customer` | Customer |
| `evangelist` | Evangelist |
| `other` | Other |

For custom lifecycle stages, the internal value is a numeric ID — you can find it in your HubSpot lifecycle stage settings or by querying the HubSpot properties API.

This behavior applies to all HubSpot enumeration properties (dropdowns, radio buttons), not just lifecycle stage.

### What happens if I update a HubSpot list or segment filter after import?

Changing a HubSpot list's membership criteria (for example, tightening segment filters so certain companies are no longer included) does **not** automatically update your Clay table. Records already imported into Clay **stay in the table** — they are not removed just because they no longer match the updated list.

To refresh your table to reflect the updated list, see [Why doesn't my Clay table update when I change the source filters?](https://www.clay.com/university/guide/sources#faqs) in the Sources guide.

### Why does my HubSpot lifecycle stage column show an internal code instead of the display label?

HubSpot's API returns internal codes for enumeration/dropdown fields rather than the human-readable labels shown in HubSpot. For example, a contact at the "Marketing Qualified Lead" stage will appear as `marketingqualifiedlead` in Clay. This applies to any HubSpot dropdown property, not just lifecycle stage.

**Workaround:** Add a Formula column that maps the internal code to the label you want to display. The default HubSpot lifecycle stage codes are:

-   `subscriber` → Subscriber
-   `lead` → Lead
-   `marketingqualifiedlead` → Marketing Qualified Lead
-   `salesqualifiedlead` → Sales Qualified Lead
-   `opportunity` → Opportunity
-   `customer` → Customer
-   `evangelist` → Evangelist
-   `other` → Other

If your HubSpot account uses custom lifecycle stages, find their internal codes in HubSpot under **Settings → Properties → Lifecycle Stage**.

### Why isn't my HubSpot Update Object populating a property that already exists in HubSpot?

If a property exists in HubSpot but doesn't get updated when you run the Update Object action, two things are worth checking:

**Blank values are silently skipped.** The **Ignore blank values** setting is enabled by default. When enabled, any property field that is empty or null in your Clay table is not sent to HubSpot — the existing HubSpot value remains unchanged with no error shown. If the column you are mapping has no value for a given row, the update for that property is skipped. To override this, open the column settings and disable **Ignore blank values** — but note that doing so will overwrite existing HubSpot data with blank values from Clay.

**A different HubSpot account is selected.** If multiple HubSpot accounts are connected to your workspace (for example, if teammates each added their own HubSpot connection), the Update Object action may be authenticating against a different instance than the one you intend to update. Open the column settings and confirm the HubSpot account shown is the correct one. You can verify by running a **Lookup object** action on the same record — if the property appears updated there, the write reached the right account.

### Why does the HubSpot Object ID field show "Required inputs missing"?

The **HubSpot Object ID** field does not auto-populate — it will always be blank when you first configure the Update object action. Unlike some other fields in Clay, no column is suggested automatically, so the action cannot run until you map a column manually.

**Fix:** Click the HubSpot Object ID field, type `/` to open the column picker, and select the column that contains your HubSpot Record IDs. Any column type — including Number — can be selected.

### Why does the Sequence dropdown show "No options found" in the "Enroll a contact in a sequence" action?

The `automation.sequences.read` scope is **disabled by default** when connecting HubSpot. Without it, Clay cannot retrieve your sequence list, so the Sequence field shows "No options found" even if you have sequences in HubSpot and have access to them.

**Fix:** A workspace admin needs to reconnect the HubSpot account with the required scopes enabled:

1.  Go to `Settings` → `Connected accounts`.
2.  Find the HubSpot account and click the `[...]` button → **Reconnect**.
3.  In the scopes selection, enable:
    -   `automation.sequences.read` — required to populate the Sequence dropdown.
    -   `automation.sequences.enrollments.write` — required to enroll contacts in a sequence.
4.  Complete the OAuth flow.

After reconnecting, the Sequence dropdown will populate with your HubSpot sequences.

**Workaround (without reconnecting):** Switch the Sequence field from **Dropdown** mode to **Text with tokens** mode and enter the sequence ID manually. You can find a sequence's ID in HubSpot under **Automation → Sequences** — it appears in the URL when you open a sequence.

### Why am I getting an `INVALID_DATE` error when writing to a HubSpot Date property?

HubSpot's Date Picker properties require values to be a Unix timestamp in **milliseconds at exactly midnight UTC** (00:00:00 UTC). Any timestamp with a time component is rejected with an error like:

```
Property values were not valid: [{"isValid":false,"message":"1641038400000 is at 12:0:0.0 UTC, not midnight!","error":"INVALID_DATE",...}]
```

Clay's **Update object** action passes date values to HubSpot exactly as provided — it does not strip the time component or normalize to midnight automatically.

**Fix:** Add a Formula column that converts the date to midnight UTC in milliseconds, then map that formula column to your HubSpot Date property:

```javascript
moment.utc({{Your Date Column}}).startOf('day').valueOf()
```

Replace `{{Your Date Column}}` with the column that holds the date you want to write (for example, the `updatedAt` field from your HubSpot import). This returns the millisecond Unix timestamp HubSpot expects.

**Avoid using the built-in Updated At column as the date source if it drives a run condition.** Clay's **Updated At** column records when a row was last modified. If an enrichment's run condition depends on **Updated At** and that enrichment writes back to HubSpot (which modifies the row), the row update refreshes **Updated At** — triggering the enrichment to run again in an infinite loop. Reference a specific data column (such as the date field from your import) instead.
