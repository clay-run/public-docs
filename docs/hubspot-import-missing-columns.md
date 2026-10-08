---
title: Why some HubSpot values don't appear as columns
description: Understand why certain HubSpot values aren't extracted into columns on import, why new HubSpot properties don't appear on existing rows, and how to surface them.
---

# Why some HubSpot values don't appear as columns

When you import records from HubSpot into Clay, you may notice that a value
exists on the record in HubSpot but doesn't appear in its own column in Clay —
especially on newly added rows. This is expected behavior, not a bug.

## The short version

When the **Import objects from HubSpot** source imports a record, Clay saves the
record with all of the HubSpot properties that existed at that moment in the
source column (the **Import object** column). But a value only appears in its
own **column** if Clay set up a column for that field. If no column exists for a
field, its value has nowhere to go — so it looks like it wasn't extracted.

The exception is a property you created in HubSpot **after** the records were
imported: that property isn't saved on rows that were already imported. See
[I created a new HubSpot property and it isn't in my Clay table](#i-created-a-new-hubspot-property-and-it-isnt-in-my-clay-table).

## Why a value might not have a column

1.  **The field wasn't part of the import when it was first set up.** Columns
    are decided when you create the import. If you later add a new property in
    HubSpot, or start using a field you weren't using before, Clay won't
    automatically create a new column for it. New rows that have that value will
    still not show it as a column. (For a property created in HubSpot after the
    import, rows that were already imported don't contain the value at all —
    see the section below.)

2.  **The field was empty on the first records Clay looked at.** When the import
    is created, Clay builds columns based on the records it sees at that moment.
    If a field was blank across those records, Clay doesn't create a column for
    it. Later, a new record might have that field filled in — but since there's
    no column for it, the value doesn't appear.

3.  **It's a calculated or read-only HubSpot field.** HubSpot fields that
    HubSpot calculates automatically (like scores or analytics fields) are not
    pulled in by default, so they don't get columns.

4.  **A new row simply doesn't have a value for that field.** If a column exists
    but a newly added record has no value for it, that cell is left blank for
    that row. Other rows may still show a value.

## How to resolve it

**Extract the value as a column from the HubSpot source column.** If the
property already existed in HubSpot when the record was imported, its value is
already saved in the **Import object** column — it just doesn't have its own
column yet.

1.  Click a cell in the **Import object** column.
2.  Find the property in the record.
3.  Click **Add as column** to extract that value into a new column.

> **Note:** For properties that existed in HubSpot at import time, you don't
> need to re-import anything — extracting the value into its own column is all
> that's needed. If you click into the **Import object** cell and the property
> isn't there, it was most likely created in HubSpot after the import — follow
> the steps in the next section.

## I created a new HubSpot property and it isn't in my Clay table

If you create a new property in HubSpot after setting up the **Import objects
from HubSpot** source, the new property won't appear on rows Clay already
imported — not in a column, and not inside the **Import object** cell. By
default, later runs of the HubSpot source (scheduled runs or **Run now**) only
pull records that were added to HubSpot since the previous run, and they don't
re-fetch records that are already in the table. Records the source imports from
then on do include the new property, because Clay loads your current list of
HubSpot properties each time the source runs.

To get the new property onto rows that are already in your table, turn on
**Update existing rows** for the HubSpot source and run it again.

### How to pull a new HubSpot property into existing rows

1.  Click the **Import object** column header and choose **Edit source**.
2.  In the source panel, open the **Run settings** section.
3.  Turn on **Update existing rows**. This setting is off by default for the
    HubSpot source. When it's on, existing rows are updated with any new
    information each time the source runs.
4.  Click **Run now**.
5.  When the run finishes, click a cell in the **Import object** column, find
    the new property, and click **Add as column** to extract it into its own
    column.

With **Update existing rows** on, the HubSpot source re-fetches every record
with your current HubSpot properties and updates the matching rows in place
(matched by HubSpot record ID) — it does not add duplicate rows.

**Update existing rows** stays on for future scheduled runs of that source. If
you only want new records on later runs, turn it off again after the run
finishes.

> **Important:** Don't add the **Import objects from HubSpot** source to the
> table a second time to pick up a new property. Each HubSpot source only checks
> for duplicates against its own records, so a second source for the same
> object adds a second row for every HubSpot record that's already in the table.

### How to remove an extra HubSpot source

If you've added the HubSpot source more than once and want to clean up the
extra copies:

1.  Click the **Import object** column header and choose **Edit source**. If
    more than one source feeds the column, pick the source you want to remove.
2.  In the source panel, click **Delete source**.
3.  If the source added rows, choose one of the following:
    -   **Delete source but keep rows** — removes the source and leaves the rows
        it imported in the table.
    -   **Delete rows** — removes the source and the rows it imported.
