---
title: Smartlead integration
source_url: https://university.clay.com/docs/smartlead-integration-overview
description: Cold email automation boosting deliverability and sales outreach.
last_synced: 2026-04-26T01:40:42.145Z
upstream_hash: 375294f05e4b473c5b06894d964df65012cc6699d250328d87aa94ae2db5d8e6
---

# Smartlead integration

Cold email automation boosting deliverability and sales outreach.

Smartlead is a cold email platform that lets sales teams run multi-inbox outreach campaigns, automate follow-up sequences, and track lead engagement at scale. Within Clay, you can push enriched leads directly into Smartlead campaigns, look up and update lead details, manage campaign statuses, and remove leads — all without leaving your workflow. Common workflows include:

-   **Outbound prospecting:** Build or import lead lists in Clay, enrich with verified contact data and personalization inputs, then push directly to Smartlead campaigns for automated outreach.
-   **Lead qualification:** Use Clay's enrichment to score and filter leads before adding them to Smartlead, ensuring only qualified prospects enter your sequences.
-   **Campaign management:** Look up lead statuses, update lead details, and remove unqualified leads from campaigns without switching tools.

## Enriching data with Smartlead

1.  While in a Clay table, click `Add enrichment` and search for `Smartlead`.
2.  Under `Integrations`, select one of the Smartlead actions.
3.  In the modal, you will be asked to `Select Smartlead account`.
    -   If you haven't already connected your account, click `+ Add account` and enter your API key. You can find your API key in your Smartlead settings at `app.smartlead.ai/app/settings/profile`.

**Note:** All Smartlead actions require an existing campaign in Smartlead. Campaigns cannot be created from within Clay — make sure your campaign is set up in Smartlead before running any action.

### `Action` Add lead to campaign

Adds a new lead to an existing Smartlead campaign.

**Inputs:**

-   `Campaign ID`: The Smartlead campaign you want to add the lead to. Displays as a dropdown populated from your Smartlead account.
-   `Email Address`: The email address of the lead.
-   `First Name (optional)`: The first name of the lead.
-   `Last Name (optional)`: The last name of the lead.
-   `Phone Number (optional)`: The phone number of the lead.
-   `Website (optional)`: The personal website of the lead.
-   `Personal LinkedIn URL (optional)`: The URL of the lead's LinkedIn profile.
-   `Location (optional)`: The lead's location (e.g., London).
-   `Company Name (optional)`: The name of the company where the lead is employed.
-   `Company URL (optional)`: The domain of the company where the lead is employed.
-   `Custom Fields (optional)`: Key-value pairs for any additional lead fields. Enter the field name on the left and the value on the right.
-   `Allow Duplicate Leads Across Campaigns? (optional)`: By default, a lead will not be added if they already exist in another Smartlead campaign. Enable this to allow a lead to appear in multiple campaigns. A lead will only be added once per individual campaign regardless.
-   `Allow Leads from Community Bounce List? (optional)`: By default, leads will be added to the campaign even if they appear on Smartlead's community bounce list (recommended for most use cases). Disable this to skip leads found on that list.

**Outputs:**

This action confirms whether the lead was successfully added but does not return additional output fields.

**Batching**

This action supports batch mode, which can be enabled via the **Run in batches** toggle in the column's **Batching** settings. When enabled, Clay groups leads that share the same Campaign ID and uploads up to 100 at a time in a single API request instead of one per row — improving throughput for high-volume campaigns and preventing the action from getting stuck in a queued state. You can adjust the **Number of rows per batch** between 1 and 100 (default: 100).

Batching boosts performance but may affect downstream tools connected to Smartlead that aren't prepared for high update volumes. Test your workflows after enabling this setting.

### `Action` Lookup lead in campaign

Retrieves lead data stored in Smartlead by searching on an email address.

**Inputs:**

-   `Email Address`: The email address of the lead to search for.

**Outputs:**

-   `Id`: The lead's internal Smartlead ID.
-   `First Name`: The lead's first name.
-   `Last Name`: The lead's last name.
-   `Email`: The lead's email address.
-   `Created At`: The date and time the lead was created in Smartlead.
-   `Company Name`: The company associated with the lead.
-   `Custom Fields`: Any custom field values stored on the lead record.
-   `Linkedin Profile`: The lead's LinkedIn profile URL.
-   `Company Url`: The domain of the lead's company.
-   `Is Unsubscribed`: Whether the lead has unsubscribed.
-   `Lead Campaign Data`: A list of all campaigns the lead is currently enrolled in.
    -   `Campaign ID`: The ID of the campaign.
    -   `Campaign Name`: The name of the campaign.

### `Action` Lookup lead status in campaign

Looks up the email-sending status of a specific lead within a Smartlead campaign.

**Inputs:**

-   `Campaign ID`: The Smartlead campaign to check. Displays as a dropdown populated from your Smartlead account.
-   `Email Address`: The email address of the lead.

**Outputs:**

-   `Lead ID`: The internal Smartlead ID of the lead.
-   `Campaign ID`: The ID of the campaign.
-   `Email`: The lead's email address.
-   `Number of Campaign Steps`: The total number of steps in the campaign sequence.
-   `Number of Sent Emails`: The number of emails that have been sent to the lead so far.
-   `Status`: The lead's current status in the campaign (e.g., `IN_PROGRESS`).

### `Action` Update lead in campaign

Updates the details of an existing lead in a Smartlead campaign.

**Inputs:**

-   `Campaign ID`: The campaign containing the lead you want to update. Displays as a dropdown.
-   `Lead ID`: The ID of the lead to update. Typically sourced from the output of a `Lookup lead in campaign` action.
-   `Email Address (optional)`: The lead's email address.
-   `First Name (optional)`: The lead's first name.
-   `Last Name (optional)`: The last name of the lead.
-   `Phone Number (optional)`: The lead's phone number.
-   `Website (optional)`: The lead's personal website.
-   `Personal LinkedIn URL (optional)`: The URL of the lead's LinkedIn profile.
-   `Location (optional)`: The lead's location.
-   `Company Name (optional)`: The company where the lead is employed.
-   `Company URL (optional)`: The domain of the company where the lead is employed.
-   `Custom Fields (optional)`: Key-value pairs for any additional lead fields.

**Outputs:**

This action confirms whether the update was successful but does not return additional output fields.

### `Action` Update lead category

Updates the category label assigned to a lead in a Smartlead campaign.

**Inputs:**

-   `Campaign ID`: The campaign containing the lead. Displays as a dropdown.
-   `Lead ID`: The ID of the lead to update. Typically sourced from the output of a `Lookup lead in campaign` action.
-   `Category ID`: The category to assign to the lead. Displays as a dropdown populated from your Smartlead account.

**Outputs:**

This action confirms whether the category was updated successfully but does not return additional output fields.

### `Action` Remove lead from campaign

Removes a lead from a Smartlead campaign.

**Inputs:**

-   `Campaign ID`: The campaign to remove the lead from. Displays as a dropdown.
-   `Lead ID`: The ID of the lead to remove. Typically sourced from the output of a `Lookup lead in campaign` action.

**Outputs:**

-   `Ok`: Returns `true` if the lead was successfully removed from the campaign.

### Run settings

-   **Auto-update:** Recommended for trigger-based workflows so that new rows added to Clay are automatically pushed to your Smartlead campaigns.
-   **Only run if:** The enrichment will only run when specified conditions are met. ([Learn more about conditional formulas here!](https://docs.clay.com/concepts/formulas/conditional-formulas))

## Best practices

-   **Qualify before adding:** Use Clay's enrichment and scoring to filter leads before pushing them to Smartlead campaigns, reducing wasted outreach on unqualified prospects.
-   **Use conditional runs:** Set conditions to only add leads that meet specific criteria (e.g., verified email, ICP match, engagement signals).
-   **Enable duplicate control thoughtfully:** By default, Smartlead prevents duplicate leads across campaigns. Only enable `Allow Duplicate Leads Across Campaigns?` when you intentionally want a lead in multiple sequences.
-   **Look up before updating:** Run `Lookup lead in campaign` first to get the Lead ID before using update or remove actions.

## Troubleshooting

### Leads are not being added to the campaign

All Smartlead actions require an existing campaign set up directly in Smartlead. If your action fails, confirm that the target campaign exists and is active in your Smartlead account before running the action again.

### Some leads weren't added when they already exist in another campaign

By default, Smartlead will not add a lead to a campaign if that lead already exists in a different Smartlead campaign. To allow the same lead to be enrolled in multiple campaigns simultaneously, enable the `Allow Duplicate Leads Across Campaigns?` toggle in the `Add lead to campaign` action. Note that a lead can only be added to each individual campaign once.

### I don't have a Lead ID to use the Update or Remove actions

The `Lead ID` required by `Update lead in campaign`, `Update lead category`, and `Remove lead from campaign` is Smartlead's internal identifier for a lead — it is not the same as a row ID in Clay. Run the `Lookup lead in campaign` action for the relevant lead first, then map the `Id` output into the `Lead ID` field of your update or remove action.
