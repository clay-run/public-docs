---
title: Table versions
source_url: https://university.clay.com/docs/table-versions
last_synced: 2026-04-26T01:40:46.704Z
upstream_hash: 09abb6a57a85c12851d9074e7152c1358b35cc6fcbe04acca14ed4b7d02ffb54
---

# Table versions

Table versioning lets you track structural changes to your Clay tables over time and restore previous configurations when needed.

Table versioning lets you track structural changes to your Clay tables over time and restore previous configurations when needed. Versions are created automatically as you work, and you can create manual snapshots before major changes — so you can always get back to a configuration that was working.

## What gets versioned

Table versions capture your table's **structure and configuration**, including:

-   Column configurations and settings
-   View configurations
-   Active filters and sorts
-   Table-level run settings

**Note:** Cell value data is not versioned. Table Versioning preserves your table’s structure and configuration—not the actual data within rows. If row-level data is overwritten or deleted, it cannot be recovered through versioning.

## Viewing your version history

1.  Click `History` in the bottom-right corner of your table.
2.  Select `All configuration versions`.

In the version viewer, you can:

-   See when each version was created.
-   Preview the table configuration at any version in read-only mode.
-   Inspect column configurations for past versions.
-   Select a version to restore.

## Creating a manual snapshot

**Tip:** Create a manual snapshot before major structural changes like column restructuring, view reorganization, or testing new column configurations.

1.  Click `History` in the bottom-right corner of your table.
2.  Select `Save configuration version` from the dropdown.
3.  Optionally add a title or description to help identify this snapshot later.
4.  Click `Create`.

Clay also creates versions automatically — a snapshot is taken after approximately 15 minutes of inactivity on a table, so you always have a version available after an editing session.

## Restoring a version

1.  Click `History` → `All configuration versions`.
2.  Select the version you want to restore.
3.  Click `Restore Configuration` to preview what the table looked like at that point.
4.  Confirm the restoration in the dialog — it will show a summary of the changes that will be applied.
5.  Click `Restore this version`.

**Note:** Restoring a version automatically creates a new snapshot of your current configuration before applying the restore — so you can always undo the operation.

### What changes when you restore

**Columns:**

-   **Added columns** — Columns added after the selected version will be removed.
-   **Updated columns** — Column settings (type, formulas, integrations, enrichment configurations) will revert to their state at the time of the snapshot. Note: updated configurations will only apply to new rows going forward. You may need to manually re-run the column to refresh existing rows and downstream dependencies.
-   **Restored columns** — Columns that existed in the selected version but were later deleted will be restored with their original configurations and any data that existed at the time of deletion.

**Sorts and filters:**

-   Active sorts and filters will revert to their state at the time of the version snapshot.

**Table settings:**

-   Auto-update and scheduled run settings will revert to their state at the time of the snapshot.
-   Version restoration does **not** affect your table's location within your workspace.
-   Version restoration does **not** affect any permission settings on your table or workbook.

## Version retention by plan

| Plan | Version history |
| --- | --- |
| Free / Trial | Not enabled |
| Growth / Launch | 30 days |
| Enterprise | 180 days |

## Troubleshooting

### My existing row data didn't change after restoring a version

Table Versioning restores **structure and configuration**, not cell-level data. If rows were overwritten or deleted before the restore, that data cannot be recovered. Additionally, restored column configurations only apply to new rows going forward — to refresh existing rows, you'll need to manually re-run the affected columns.

### I can't find a version from a specific date

Version history is retained based on your plan (30 days for Launch/Growth, 180 days for Enterprise). Versions outside your retention window are no longer available. If you're on a Free or Trial plan, version history is not enabled.

### Restoring a version removed columns I still needed

Restoring a version removes columns that were added after the snapshot was taken. Because the restore operation automatically creates a new snapshot of your configuration immediately before applying the restore, you can recover by restoring that most-recent pre-restore version.
