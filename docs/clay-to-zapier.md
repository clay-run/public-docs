---
title: Send Clay data to Zapier
source_url: https://university.clay.com/docs/clay-to-zapier
last_synced: 2026-04-26T01:39:44.880Z
upstream_hash: d60164e2291327206e08f6b1072323fa834b53905358076df2f33edc694f052f
---

# Send Clay data to Zapier

Use webhooks to send Clay data to trigger Zapier workflows.

With HTTP API, you can send data from your Clay table to Zapier to trigger workflows.

To do this, we’ll take advantage of [Zapier webhooks](https://zapier.com/apps/webhook/integrations)!

## Setting up Zapier

To begin, we'll first set up a Zapier webhook which is going to "catch" your Clay data.

1.  Create a new Zap.
2.  Click `Trigger` and select `Webhooks`.
3.  Under `Trigger event` select `Catch Hook`.
4.  Under `Test`, copy the webhook URL.
5.  Finish the Zap by setting up an `Action`.
    -   While you'll need to complete this step to publish the Zap, it's not essential for creating the webhook, so you can choose any action.

### Adding to Clay

Now that you’ve created your Zap, you’ll need to paste the webhook URL into a Clay table.

1.  Navigate to your Clay table, click `Add enrichment` and search for `HTTP API`.
2.  For `Method` → `POST`.
3.  Paste the webhook URL into `Endpoint`.
4.  In the `Body` section, include the data from your table that you want to use in your Zap, formatted in JSON.
    -   You can use dynamic column names so that each of your rows gets sent to Zapier separately.
5.  Click `Save` → `Save and run`. A `200` response in the column cell confirms that your webhook successfully sent the data to Zapier.
