---
title: Send Clay data to Zapier
description: Use webhooks to send Clay data to Zapier, or troubleshoot Zapier's native Clay integration.
last_synced: 2026-04-26T01:39:44.880Z
---

# Send Clay data to Zapier

Use webhooks to send Clay data to trigger Zapier workflows.

With HTTP API, you can send data from your Clay table to Zapier to trigger workflows.

To do this, we'll take advantage of [Zapier webhooks](https://zapier.com/apps/webhook/integrations)!

## Setting up Zapier

To begin, we'll first set up a Zapier webhook which is going to "catch" your Clay data.

1.  Create a new Zap.
2.  Click `Trigger` and select `Webhooks`.
3.  Under `Trigger event` select `Catch Hook`.
4.  Under `Test`, copy the webhook URL.
5.  Finish the Zap by setting up an `Action`.
    -   While you'll need to complete this step to publish the Zap, it's not essential for creating the webhook, so you can choose any action.

### Adding to Clay

Now that you've created your Zap, you'll need to paste the webhook URL into a Clay table.

1.  Navigate to your Clay table, click `Add enrichment` and search for `HTTP API`.
2.  For `Method` → `POST`.
3.  Paste the webhook URL into `Endpoint`.
4.  In the `Body` section, include the data from your table that you want to use in your Zap, formatted in JSON.
    -   You can use dynamic column names so that each of your rows gets sent to Zapier separately.
5.  Click `Save` → `Save and run`. A `200` response in the column cell confirms that your webhook successfully sent the data to Zapier.

## Using Zapier's native Clay integration

Zapier offers a native Clay connector with a **Create Record in Table** action that lets you add rows to a Clay table directly from a Zap. When configuring it, Zapier prompts you to select a Workspace — if the dropdown shows **"No options are available"**, enter your Workspace ID manually:

1.  Open your Clay workspace in the browser.
2.  Copy the numeric ID from the URL — it appears after `workspaces/`:
    `https://app.clay.com/workspaces/YOUR-ID-HERE/`
3.  In Zapier, select **Custom** and paste the ID.

You can find Table IDs and View IDs the same way: they appear after `tables/` and `views/` in the URL.

### Confirming your API key

If your workspace still doesn't appear after entering the ID manually, verify that you're using the correct Clay API key:

-   In Clay, go to `Settings` → `Account` → `API key`.
-   Copy the key and re-enter it in Zapier's Clay connection settings.

### Webhook alternative (Growth plan and above)

If the native Zapier integration continues to have issues, you can route data into Clay via a webhook instead, bypassing workspace and table selection entirely:

1.  In Clay, create a table using **Monitor webhook** as the source and copy the webhook URL. Webhooks are available on Growth plan and above — see [Webhooks in Clay](webhook-integration-guide.md) for setup details.
2.  In Zapier, add a **Webhooks by Zapier** action and select **POST**.
3.  Paste your Clay webhook URL and configure the JSON payload with the fields you want to send.
