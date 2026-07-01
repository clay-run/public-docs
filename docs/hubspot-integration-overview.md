---
title: HubSpot integration
description: All-in-one CRM platform for marketing, sales, and customer service.
last_synced: 2026-04-26T01:40:09.362Z
---

# HubSpot integration

All-in-one CRM platform for marketing, sales, and customer service.

HubSpot is a customer relationship management (CRM) platform that helps businesses manage sales, marketing, and customer service.

With this integration, you can import, create, update, and manage HubSpot objects directly in Clay.

**Heads up!** The HubSpot integration requires a **Growth plan** or higher. See [Plans & billing](plans-and-billing.md) for details.

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

-   **Object type:** The type of HubSpot object to create (Contact, Company, Deal, Lead, or a custom object type).
-   **Properties:** After selecting an object type, HubSpot's writable properties load dynamically. Map each Clay column to the HubSpot property you want to populate (for example, map your company name column to `name` and your domain column to `domain`).

**Note:** For Contact, Company, Deal, and custom objects, associating a created record with another HubSpot object (for example, linking a contact to a company) is not part of the Create Object step — it requires a separate **Create association** action. See [How do I create a contact-to-company association in HubSpot from Clay?](#how-do-i-create-a-contact-to-company-association-in-hubspot-from-clay) for a step-by-step workflow. **Lead is an exception:** when **Object type** is set to Lead, the Create Object step includes required association fields (**Association Object Type**, **Association Type**, and **To Object ID**) directly, so a Lead is always created with an association in the same step.

### `Action` Lookup object

Use this action to look up an object in HubSpot.

**Inputs**

-   **Object type:** The type of HubSpot object to look up.
-   **Fields to filter by:** The HubSpot properties to search against (e.g., select `Domain Name` to find a company by domain, or `Email` to find a contact by email address). Available filter fields are loaded dynamically based on the selected object type.
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

### How often does my HubSpot source update, and how do I refresh it immediately?

The update frequency is set by the run schedule you configure in Clay — not by any schedule within HubSpot itself. Options include daily, weekly, and monthly; hourly is available on some plans. To view or change the schedule, click the source column title, select your source, and check the **Run settings** section.

To pull the latest HubSpot data immediately without waiting for the next scheduled run, click the source column title, select your source, and click **Run now**. This triggers a fresh source execution and updates your table with the current state of the HubSpot list.

### When I schedule my HubSpot list source to refresh, does it pick up removals from the list?

**No — scheduled refreshes are additive only.** When a HubSpot list source runs on a schedule, it adds new records from the list to your Clay table but does not remove records that have since been dropped from the list. Records stay in your table even after they are no longer members of the HubSpot list in HubSpot.

**Schedule options:** The default frequency when setting up a scheduled source is daily. You can also choose weekly or monthly. To set or change the schedule, click the source column title, select your source, and choose **On a schedule** under **Run this source**. For all available intervals and plan requirements, see [Scheduled sources](https://www.clay.com/university/guide/scheduled-sources).

**If your HubSpot list rotates periodically** (for example, a quarterly suppression or exclusion list that gets replaced with a new list), a scheduled refresh of the existing source will not remove the old records. To get a clean slate:

-   **Create a new table** from the updated list — this starts a fresh import containing only the current list members.
-   **Manually delete** the rows you want to remove from the existing table, then re-run the source to pull in any new additions.

For more on additive source behavior across all source types, see [Will rows already in my table be removed if they no longer match the source filter?](https://www.clay.com/university/guide/sources#will-rows-already-in-my-table-be-removed-if-they-no-longer-match-the-source-filter) in the Sources guide.

### My HubSpot list has more than 50,000 records — how do I process all of them?

The **Import objects from HubSpot** source is limited to 50,000 records. Enabling auto-delete does not bypass this limit for HubSpot imports — auto-delete only resets the record count for webhook and send-table-data sources, not for CRM imports.

For large, one-time batch processing (for example, 100k companies), use [Bulk Enrichment](bulk-enrichment.md) instead of a standard table:

1. Export your HubSpot list to CSV from HubSpot.
2. Create a Bulk Enrichment table (`New` → `Bulk enrichment`) and select **Import from CSV** as the source type.
3. Configure your enrichment columns and run.

Bulk Enrichment handles large datasets without the 50,000-row limit. Note that HubSpot is not yet available as a direct Bulk Enrichment CRM import source (Salesforce and CSV only today); exporting to CSV first is the current workaround.

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

### Why do I get a "property values were not valid" error when pushing to a HubSpot dropdown property?

When you use **text with tokens** to map a dynamic Clay column value to a HubSpot dropdown (enumeration) property, HubSpot validates the string against its accepted internal option values — and the match is case-sensitive. Clay passes your mapped value to HubSpot's API as-is, without any case transformation or label-to-value mapping.

**HubSpot's built-in dropdown properties store their internal values in ALL CAPS.** For example, the Industry property's internal value for "Design" is `DESIGN`, not `Design`. Passing the display label or a mixed-case string returns a `property values were not valid` error even when the value looks correct to you in HubSpot's UI.

**To find the correct internal values for a dropdown property:**

- Use Clay's **Lookup object** action on a record where the property is already populated in HubSpot. The raw value returned (e.g., `DESIGN`, `INFORMATION_TECHNOLOGY_AND_SERVICES`) is the internal value you must pass.
- Or open **Settings → Properties** in HubSpot, select the property, and check each option's internal name — that is what HubSpot's API expects.

**Mapping enriched industry values to a dropdown**

Clay's Native Company Enrich aggregates industry data from multiple underlying providers (Clearbit, Apollo, Owler, HG Insights, and others), each using its own taxonomy. Because the exact industry string returned varies by provider and per row, there is no single fixed list of values. Before pushing to a HubSpot dropdown, add a **Use AI** or Formula column to normalize the raw enriched value to one of your HubSpot dropdown's internal option names. For example, a Use AI column can classify an enriched industry string into one of your defined dropdown option names, and a Formula column can apply `.toUpperCase()` to ensure the casing matches HubSpot's expected format.

If your use case requires storing free-form industry values that don't map to a fixed set of options, consider using a **plain text property** in HubSpot instead.

### Why isn't my HubSpot Update Object populating a property that already exists in HubSpot?

If a property exists in HubSpot but doesn't get updated when you run the Update Object action, two things are worth checking:

**Blank values are silently skipped.** The **Update Object** action has an **Ignore blank values** setting that is enabled by default. When enabled, any property field that is empty or null in your Clay table is not sent to HubSpot — existing HubSpot values are left unchanged with no error shown. If the column you are mapping has no value for a given row, the update for that property is skipped. To override this, open the column settings and disable **Ignore blank values** — but note that doing so will overwrite existing HubSpot data with blank values from Clay. (This setting applies only to the Update Object action; the Create Object action does not have an equivalent option.) **Note:** If *every* property mapped in that column is blank for a row, the column shows a "No properties found to update" error rather than silently skipping — see the FAQ below for how to address this with a run condition.

**A different HubSpot account is selected.** If multiple HubSpot accounts are connected to your workspace (for example, if teammates each added their own HubSpot connection), the Update Object action may be authenticating against a different instance than the one you intend to update. Open the column settings and confirm the HubSpot account shown is the correct one. You can verify by running a **Lookup object** action on the same record — if the property appears updated there, the write reached the right account.

### Why does my HubSpot Update Object show "Required inputs missing" after I deleted a column?

If the column that was previously mapped to the **HubSpot Object ID** field has been deleted from the table, the field retains a stale reference to that removed column. The action sees this as a missing required input and will not run.

**To reconnect:**

1.  Open the Update object column's settings.
2.  Click the **HubSpot Object ID** field — the broken reference will appear in the input.
3.  Clear the existing value, then type `/` to open the column picker and select the column that contains your HubSpot Record IDs.

**Tip:** The most reliable source for the HubSpot Object ID is the `hs_object_id` value returned by a HubSpot **Import source** or **Lookup object** action on the same table. If you are using a plain text column of IDs (for example, values imported from a CSV), the column type does not matter — but the values must exactly match the HubSpot Object IDs of the records you want to update.

### Why does my HubSpot Update Object show "Object not found"?

This error means the value mapped to the **HubSpot Object ID** field is not a valid HubSpot record ID. The most common cause is mapping an email address (or another non-ID value such as a domain or name) to this field. HubSpot's API expects a numeric internal record ID and responds with *"Object not found. objectId are usually numeric"* when any other value is passed.

**To fix:**

1. Open the **Update object** column's settings.
2. Click the **HubSpot Object ID** field and replace the current mapping with a column containing the numeric `hs_object_id` value.

**Where to get `hs_object_id`:**

- **If you imported contacts via Import objects from HubSpot:** The `hs_object_id` field is included in the import result. Select that column.
- **If you don't have the ID yet:** Add a **HubSpot → Lookup object** column before your update step — filter by **Email**, then map the `hs_object_id` from the Lookup result to the **HubSpot Object ID** input in the Update object column.

**Note:** Email addresses cannot be used as a HubSpot Object ID. Use **Lookup object** to find a record by email and retrieve its `hs_object_id`, then pass that value to **Update object**.

### Why do I get "Missing input: Please provide at least one filterable field" when setting up Lookup Object?

This error means you've selected a field to filter by but haven't mapped a value to it yet. The **Lookup Object** setup requires two steps:

1. Under **Fields to filter by**, select a HubSpot property to search against (e.g., **Domain Name** to find a company by domain, or **Email** to find a contact by email address).
2. After you select a field, a new value input appears for that field. Map it to the column in your table that contains the value you want to search for (e.g., your domain column or email column).

Both steps are required — the action needs to know which field to search AND what value to look for. If you select a filter field but leave its value input unmapped, the action can't run and shows this error.

**Tip:** For contacts, **Email** is the most reliable filter field because it's the primary identifier HubSpot uses for contact lookups.

### How do I create a contact-to-company association in HubSpot from Clay?

Use the **Lookup object** and **Create association** actions together in your contacts table — you don't need Send table data for this workflow.

**Step 1 — get the company's `hs_object_id` onto each contact row**

Add a **HubSpot → Lookup object** column to your contacts table:

1.  Set **Object type** to **Company**.
2.  Under **Fields to filter by**, select **Domain Name** (or another shared identifier like email domain).
3.  Map the filter value to the domain column on your contacts table.

This returns the matching company record directly on each contact row, with `hs_object_id` surfaced at the top of the result.

**Step 2 — create the association**

Add a **HubSpot → Create association** column:

-   **From object type**: Contact
-   **To object type**: Company
-   **Association type**: select the appropriate relationship (e.g., "Contact to Company")
-   **From Object ID**: your contact's `hs_object_id` (from your HubSpot contacts source column)
-   **To Object ID**: the `hs_object_id` returned by the Lookup object column in step 1

**Note:** The **From Object ID** and **To Object ID** fields appear only after you have selected both object types and an association type.

### Why does my Lookup Object return no results, but my Create Object still fails with "contact already exists"?

This almost always means the **Lookup Object** and **Create Object** columns are searching and writing to **different email fields**. HubSpot has two separate email properties:

-   **Email** (`email`) — the primary contact email address.
-   **Work email** (`work_email`) — a separate secondary property for professional email.

If your Lookup Object filters by "Work email" but your Create Object maps data to the standard "Email" property (or vice versa), the lookup will return no results while the create still fails with a duplicate error — the same address already exists under the other field.

**Fix:** Open both column settings and confirm they reference the **same email property**. If your contacts in HubSpot are stored under "Email," update your Lookup Object to filter by "Email" rather than "Work email."

**Setting up a create-or-update (upsert) workflow**

To handle both new and existing contacts without hitting duplicate errors:

1.  Add a **Lookup object** column. Configure it to search by the same identifier (e.g., email address) and the same field you write to when creating contacts.
2.  Add a **Create object** column. In **Run settings**, open **Only run if** and add a condition that the ID field returned by your Lookup column is empty — this ensures Create only runs for rows where no existing contact was found.
3.  *(Optional)* Add an **Update object** column for existing contacts. Set an **Only run if** condition to check that the Lookup column returned a result, and map the returned contact ID to the **HubSpot Object ID** input.

For full details on writing run conditions, see [Conditional runs](https://university.clay.com/docs/conditional-runs).

### Why do I get an `INVALID_OWNER_ID` error when setting `hubspot_owner_id`?

HubSpot uses two separate identifiers for each user who can own a contact:

-   **Owner ID** — the value used for the `hubspot_owner_id` contact property. This is the `id` field returned by HubSpot's Owners API (`/crm/v3/owners`).
-   **User ID** — HubSpot's internal account ID for the same person, which appears in contexts like HubSpot's Settings → Users & Teams.

These two values are sometimes identical and sometimes different. Passing a user ID where an owner ID is expected returns an `INVALID_OWNER_ID` error, even though the ID appears valid in HubSpot.

**Fix:** Use Clay's **Find owner** action to look up the owner by email address. The `id` field in the returned result is the correct owner ID to pass as `hubspot_owner_id` in an Update Object action.

Also, keep the column storing the owner ID as a **Text** type in Clay, not a **Number** type. HubSpot's API expects owner IDs as strings — passing a numeric value can cause type-mismatch errors.

### Why is my HubSpot Owner ID column blank in Clay?

A blank Owner ID column in Clay means the corresponding contact (or other object) in HubSpot does not have an owner assigned. Clay reflects the data present in HubSpot at the time of import — if no owner is set on the record in HubSpot, the Owner ID field will be empty in Clay.

**To resolve:**

1. Open the record in HubSpot and confirm whether an owner is set on the contact.
2. If no owner is assigned, set the owner directly in HubSpot.
3. Once updated in HubSpot, re-run the relevant column in Clay (for example, your **Import objects** source column or a **Lookup object** enrichment) to pull in the updated value.

**Note:** This is different from the `INVALID_OWNER_ID` error, which occurs when an owner *is* set but the wrong identifier type is passed when writing back to HubSpot. See [Why do I get an `INVALID_OWNER_ID` error?](#why-do-i-get-an-invalid_owner_id-error-when-setting-hubspot_owner_id) for that scenario.

### Why does my HubSpot column still show "Missing authentication" after I reconnect my account?

Each HubSpot column stores a reference to the specific connection it was configured with at creation time. If you **delete** your HubSpot connection and **add a brand-new one**, the new connection gets a new internal ID — but your existing columns still reference the old (now deleted) connection ID. The columns continue to show "Missing authentication" even though the new connection shows **Success** in Settings.

**To avoid this in the future:** When troubleshooting HubSpot authentication, use the **Reconnect** option on your *existing* connection instead of deleting it and adding a new one. In **Settings → Integrations → HubSpot**, click the `···` menu next to your connection and choose **Re-authenticate** or **Update connection**. This refreshes the credential while keeping the same connection ID that your existing columns already reference.

**To fix columns that are already broken:**

1. Open each affected column's settings and change the **Account** dropdown to select the new connection. This updates the column to use the new connection ID.
2. If re-selecting the account in the existing column doesn't resolve the error, create a new column with the same HubSpot action and configuration. New columns automatically pick up the currently active connection and will run successfully.

### Why does my HubSpot Create Object show "Invalid input" on some rows?

When a row is missing a required input — for example, the company ID needed to associate a new Lead with a company — Clay shows an **"Invalid input"** error for that row (e.g., *"Invalid input: Please provide all association fields"*). This error is separate from authentication errors: it means the row does not have the data needed to complete the create request.

**Fix:** Add a run condition so the action only runs on rows where the required field is populated. Open the column settings, go to **Run settings → Only run if**, and add a condition that checks the required input field is not empty. Rows without the required value will be skipped cleanly without showing an error.

**Tip:** If you see both "Missing authentication" and "Invalid input" errors in the same column, resolve the authentication issue first (see the FAQ above), then re-run the column to identify which remaining errors are due to missing field values.

### Why does my HubSpot Update Object show "No properties found to update" when Ignore blank values is enabled?

This error appears when **every** property mapped in that column is blank for a given row. When **Ignore blank values** is enabled (the default), Clay strips all blank fields from the payload before sending to HubSpot. If every mapped field is blank, nothing is left to send — and HubSpot returns "No properties found to update," which Clay surfaces as an error in the cell.

This is different from the case where some mapped fields have values: when at least one field is populated, the blank fields are simply skipped and the non-blank ones are sent to HubSpot normally.

**Fix:** Add a run condition so the column only fires when the source input has a value. Open the column settings, go to **Run settings → Only run if**, and add a condition that checks the mapped source field is not empty. Rows with no value will be cleanly skipped with no error.

**Note:** The older **Update Contact** and **Update Company** actions handle this case differently — they return a success result with "Nothing to update" instead of an error. If you previously used one of those actions and recently switched to **Update Object**, this difference in behavior is expected.

### Why do HubSpot property fields not appear in the Update Object mapping section?

When you open an **Update Object** column and select an **Object type**, the available HubSpot properties are fetched from your HubSpot account in real time. If the field picker is empty or the mapping section shows no properties, check the following:

**The fields may still be loading.** Property lists are retrieved from HubSpot's API asynchronously — wait a few seconds after selecting the Object type before assuming something is wrong. If nothing appears after waiting, close and reopen the column settings to trigger a fresh fetch.

**The HubSpot connection may be missing required OAuth scopes.** Clay uses the `crm.schemas.companies.read` and `crm.schemas.contacts.read` scopes to load property lists for Company and Contact objects (for deals, `crm.schemas.deals.read` is also required). If these scopes were not granted when you first connected HubSpot, the field picker returns no properties. To fix this, open **Settings → Integrations → HubSpot**, click the `···` menu next to your connection, and choose **Re-authenticate** — this re-requests the full scope set without changing your connection ID or breaking existing columns.

**The connection may be broken or expired.** If Clay cannot reach HubSpot with a valid access token, the field picker silently returns no properties. Open the column settings and verify the selected account shows **Success** in Settings. If it shows an error, see the FAQ above ("Why does my HubSpot column still show 'Missing authentication' after I reconnect my account?") for how to restore the credential without losing your column configurations.

### How can I create HubSpot notes from Clay?

Clay's HubSpot integration does not include a native action for creating Notes. To create notes from Clay, use the **HTTP API** integration with a HubSpot Private App token to call HubSpot's CRM objects endpoint directly.

**Setup:**

1. In your Clay table, add an **HTTP API** column.
2. Set the **Method** to `POST` and the **URL** to `https://api.hubapi.com/crm/v3/objects/notes`.
3. Add an `Authorization` header set to `Bearer <your-private-app-token>`.
4. In the request body, include a `properties` object with the fields you want to populate:
   - `hs_timestamp` — the date and time of the note in ISO 8601 format (e.g. `2024-01-15T10:00:00Z`)
   - `hs_note_body` — the text content of the note
   - `hubspot_owner_id` — optional; the HubSpot owner to assign the note to. Use Clay's **Find owner** action to get the correct owner ID.
5. To associate the note with an existing contact, deal, or other HubSpot object, include an `associations` array in the request body. For a note-to-contact link, use HubSpot association type `202`.

**Tip:** Use the `hs_object_id` returned by a HubSpot **Lookup object** column to get the correct object ID for the association target.

If a note you created does not appear in HubSpot, confirm that your HubSpot role has permission to view unassigned notes and that your HubSpot view filter includes notes.
