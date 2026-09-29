---
title: Canva integration
description: Turn rows into on-brand Canva designs — fill brand templates with Clay data, upload images from a URL, and export designs as files.
last_synced: 2026-09-29T00:00:00.000Z
---

# Canva integration

Turn rows into on-brand Canva designs — fill brand templates with Clay data, upload images from a URL, and export designs as files.

The Canva integration connects Clay to your Canva workspace, letting you generate personalized, on-brand designs at scale. Use it to fill brand templates with row data, upload assets, export designs in multiple formats, and retrieve design analytics.

## Using Canva in Clay

1.  While in a Clay table, click `Add enrichment` and search for `Canva`.
2.  Under `Integrations`, select one of the Canva actions.
3.  In the modal, click `+ Add account` and connect your Canva account via OAuth.

### `Action` Autofill brand template

Fill a Canva brand template with data from the row and create a new design. Pick a template, then map Clay columns to its text, chart, and sheet fields. Image fields take a Canva asset ID (use the Upload asset from URL action first to get one). Returns the new design's ID, title, edit URL, and view URL.

**Note:** Requires the connected user to be in a Canva Enterprise organisation.

**Inputs**

-   **Brand template (Required):** Select the Canva brand template to fill. Only templates with autofill fields are listed.
-   **Design title (Optional):** Title for the new design. Defaults to the template's title.
-   **Template fields:** Map Clay columns to the template's autofill text, chart, and sheet fields.

### `Action` Upload asset from URL

Upload an image or video from a URL in the row into the connected user's Canva assets. Returns an asset ID that you can use in the Autofill brand template image fields.

**Inputs**

-   **URL (Required):** The image or video URL to upload.

### `Action` Get design

Returns the metadata for a Canva design: title, owner, page count, thumbnail, created and updated timestamps, and the edit and view URLs.

**Inputs**

-   **Design ID (Required)**

### `Action` Export design

Exports a Canva design as a file and returns the download URL. Supported formats: `jpg`, `png`, `gif`, `pptx`, `mp4`, `pdf`, `csv`, `html_bundle`, and `html_standalone`.

**Note:** The download URL expires after 24 hours. Save the file rather than the link if you need it to persist.

**Inputs**

-   **Design ID (Required)**
-   **Format (Required):** The file format to export.

### `Action` Get design analytics

Returns view analytics for a design — total views and unique viewers over the reporting period.

**Note:** Requires the connected user to be in a Canva Enterprise organisation.

**Inputs**

-   **Design ID (Required)**
-   **Date range:** The period to retrieve analytics for.

### `Source` List Canva designs

Pull your connected user's Canva designs into a Clay table, with ID, title, thumbnail, page count, and Canva URLs.

**Currently in beta — contact support to enable.**
