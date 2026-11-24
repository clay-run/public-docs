---
title: Why some HubSpot values don't appear as columns
description: Understand why certain HubSpot values aren't extracted into columns on import, and how to surface them.
---

# Why some HubSpot values don't appear as columns

When you import records from HubSpot into Clay, you may notice that a value
exists on the record in HubSpot but doesn't appear in its own column in Clay —
especially on newly added rows. This is expected behavior, not a bug.

## The short version

Clay saves the **entire** HubSpot record when it imports it, so the value is not
lost. But a value only appears in a **column** if Clay set up a column for that
field. If no column exists for a field, its value has nowhere to go — so it
looks like it wasn't extracted.

## Why a value might not have a column

1.  **The field wasn't part of the import when it was first set up.** Columns
    are decided when you create the import. If you later add a new property in
    HubSpot, or start using a field you weren't using before, Clay won't
    automatically create a new column for it. New rows that have that value will
    still not show it as a column.

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

**Extract the value as a column from the HubSpot source column.** The full
record is already saved in your HubSpot source column, so the value you're
looking for is already there — it just doesn't have its own column yet. Use the
source column to extract that value into a new column.

> **Note:** You don't need to re-import or re-sync anything. Because the value
> already lives in the source column, extracting it into its own column is all
> that's needed.
