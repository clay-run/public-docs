---
title: Enriching records with Workflows
description: Use Workflows to enrich records from CSV files and Audience segments, and reuse data from a bulk enrichment's archived runs.
last_synced: 2026-04-27T18:09:27.586Z
---

# Enriching records with Workflows

Use [Workflows](https://university.clay.com/docs/workflows) to enrich records and send the results to your destination. Start with a CSV upload or connect a workflow to an Audience segment.

For setup, triggers, testing, and publishing, see [Workflows](https://university.clay.com/docs/workflows). To enrich records already in Audiences, see [Adding enrichments](audiences.md#adding-enrichments) and [Connecting a workflow to a segment](audiences.md#connecting-a-workflow-to-a-segment).

## Can I unarchive a bulk enrichment's archived run?

No. A bulk enrichment's archived run can't be unarchived or restored as an editable table. When you open a bulk enrichment's archive with **View archive** and pick a run, the run opens as a view-only table labeled **Archived run (date @ time)**, for example **Archived run (10/29/26 @ 1:18:14 PM)**. In an archived run you can browse and search the rows, but you can't edit its columns, and other tables can't reference or look up the archived run's data.

The archived run view loads up to 1,000 rows. The toolbar shows how many rows are loaded out of the run's total, for example **Viewing 1,000 / 255,923 rows**. To get every row of the archived run, click **Export full archive** in the toolbar to download it as a CSV file.

**Note:** This is different from archiving Audience records. Archived Audience records can be restored from the **Archived** section in Audiences — see [How do I remove records from an audience?](audiences.md#how-do-i-remove-records-from-an-audience).

## How do I reuse data from a bulk enrichment's archived run in another table?

To reuse enriched values from a bulk enrichment's archived run — for example, a company's headquarters location — without re-running the enrichment on every record, export the archived run and write the values to your Audience records from a Clay table. The **Update Audiences record** action requires Audiences on your workspace (Launch, Flex, Growth, and Enterprise plans).

1.  Open the archived run and click **Export full archive** to download it as a CSV file.
2.  Remove any columns you don't need from the CSV, but keep the **Audiences ID** column. Clay uses the Audiences ID to find the record to update.
3.  Import the CSV into a Clay table.
4.  In the table, click **Add enrichment** and add the **Update Audiences record** action.
5.  Map the **Audiences ID** column as the record ID, then map each column you want to keep to the Audience field it should update.
6.  Run the column. The values are saved on the existing Audience records, where you can filter on them in segments or pull them into other tables with `Lookup in Audiences`.

**Update Audiences record** only updates records that already exist in your Audience and only writes to Audience fields that already exist — see [Adding enrichments](audiences.md#adding-enrichments) for how it differs from `Upsert Audiences Record`.
