---
title: Troubleshoot "Share" URLs in professional post Signals and integrations
description: Fix errors in the Get interactions with professional posts Signal and
  the Get comments on a professional post integration caused by LinkedIn "Share" URLs.
---

# Troubleshoot "Share" URLs in professional post Signals and integrations

Fix errors in the Get interactions with professional posts Signal and the Get comments on a professional post integration caused by LinkedIn "Share" URLs.

## Applies to

- **Signal:** Get interactions with professional posts
- **Integration:** Get comments on a professional post
- (and the related Get reactions on a professional post integration)

## The problem

These integrations require a standard professional **post URL**. When a row contains a **"Share" URL** instead, the integration can't resolve the post and the row errors out or returns no results.

A Share URL is any LinkedIn post URL that has the word **`share`** in it, for example:

```
https://www.linkedin.com/feed/update/urn:li:share:7123456789012345678/
```

Because Share URLs point to a different URN type than the integrations expect, they need to be converted to the correct post URL before the Signal or the comments/reactions integrations will run successfully.

## The fix (overview)

Run the **Enrich professional post** integration on any row that contains a Share URL. Its output gives you the correct post URL, which you then use in your Signal and in your Get comments / Get reactions integrations.

To avoid spending credits on rows that don't need it, first flag which rows actually contain a Share URL, and run the enrichment **only** on those rows using a conditional run formula.

> **Cost note:** Running **Enrich professional post** costs **0.5 credits per row**. The steps below ensure you only spend credits on rows that actually contain a Share URL.

## Step-by-step

### Step 1 — Flag the rows that contain a Share URL

Create a **Formula column** that checks whether the LinkedIn Post URL contains the word `share` and returns `True` if it does.

Example formula (replace `(column name)` with the name of your LinkedIn Post URL column):

```
/(column name) contains "share"
```

- Rows with a Share URL → `True`
- All other rows → `False`

Name this column something clear, like **`Is Share URL`**.

### Step 2 — Run "Enrich professional post" on the flagged rows only

Add the **Enrich professional post** integration and point it at your LinkedIn Post URL column.

Before running, set a **conditional run formula** so the integration only runs when the flag from Step 1 is `True`:

```
/Is Share URL contains "True"
```

This way the enrichment (and the 0.5-credit charge) only applies to rows that actually contain a Share URL.

### Step 3 — Use the corrected URL in your Signal and integrations

The **Enrich professional post** output includes the **correct post URL**. Use that corrected URL (instead of the original Share URL) as the input for:

- **Get interactions with professional posts** (Signal)
- **Get comments on a professional post**
- Get reactions on a professional post

Tip: If some rows already had valid post URLs (flag = `False`), you can use a formula or a column mapping to pass through the original URL for those rows and the enriched URL for the Share-URL rows — so every row feeds a valid post URL into the downstream integrations.

## Quick checklist

- [ ] Formula column added that returns `True` when the URL contains `share`
- [ ] Enrich professional post integration added, with a conditional run formula on `True` rows only
- [ ] Downstream Signal / comments / reactions integrations point at the corrected post URL
- [ ] Confirmed credit spend (0.5 credits/row) is limited to Share-URL rows

## FAQ

**How do I know I had a Share URL in the first place?**
The URL contains the word `share` (e.g. `urn:li:share:...`). Standard post URLs the integrations expect do not.

**Do I need to run Enrich professional post on every row?**
No. Use the flag from Step 1 plus a conditional run formula so it only runs on Share-URL rows. This limits credit spend.

**How much does this cost?**
Enrich professional post is **0.5 credits per row** it runs on.
