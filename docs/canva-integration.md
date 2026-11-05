---
title: Canva integration
description: Use the Canva integration to autofill brand templates with row data, upload assets, export designs as files, and import Canva designs into a table.
last_synced: 2026-09-28T16:56:51.075Z
---

# Canva integration

Turn rows into on-brand Canva designs, export them as files, and pull your designs and their details into Clay.

Canva is an online design platform for creating graphics, presentations, and videos. With this integration, you can fill a Canva brand template with each row's data to give every row its own design, then export those designs as files or look up their details. A brand template is a Canva template set up with autofill fields, which are placeholders for text, images, and charts.

## **Creating a table with Canva**

1.  In a workbook, click `+ Add` at the bottom.
2.  Search for `Canva` and select `List Canva designs` from the results.
3.  In the modal, you will be asked to `Select Canva account`.
    -   If you haven't already connected your Canva account, click `+ Add account` and sign in to the Canva account you want Clay to use. Clay works as that Canva user, so the designs and brand templates you can use are the ones that account can access, and uploads land in that account.

### `Source` List Canva designs

Import the connected account's Canva designs into a table, with one row per design.

**Inputs**

All inputs are optional.

-   **Search term:** Only import designs that match this search term. Leave it empty to import every design.
-   **Ownership:** Which designs to import: `Owned designs` for designs the account owns, `Shared designs` for designs shared with it, or `All designs` for both. Defaults to `All designs`.
-   **Sort by:** The order designs are imported in: `Recently modified first`, `Oldest modified first`, `Relevance`, `Title A-Z`, or `Title Z-A`. Defaults to `Recently modified first`.
-   **Result limit:** The most designs to add to the table, up to 10,000. Defaults to 1,000.

**Outputs**

The source creates the following columns:

-   **Design ID:** The design's Canva ID, which `Export design`, `Get design`, and `Get design analytics` take as input.
-   **Design title:** The design's title.
-   **View URL:** A link to view the design in Canva.
-   **Edit URL:** A link that opens the design in the Canva editor.
-   **Thumbnail URL:** A link to the design's thumbnail image.
-   **Page count:** How many pages the design has.
-   **Created at:** When the design was created.
-   **Updated at:** When the design was last updated.

## **Enriching data with Canva**

1.  While in a Clay table, click `Add enrichment` and search for `Canva`.
2.  Under `Integrations`, select one of the Canva actions.
3.  In the modal, you will be asked to `Select Canva account`.

**Note:** To use `Autofill brand template` or `Get design analytics`, the connected Canva account needs to belong to a Canva Enterprise organization.

### `Action` Autofill brand template

Fill a Canva brand template with a row's data to create a new design.

**Inputs**

Required:

-   **Brand template:** The brand template to fill. Only templates with autofill fields appear in the list, so add those fields to the template in Canva first.
-   **Template fields:** One input for each autofill field on the template, named as it is in Canva. Map a column or value to at least one of them. What each field accepts depends on its type:
    -   **Text fields:** Any text.
    -   **Image fields:** The Canva asset ID of an uploaded image, such as `Msd59349ff`, rather than an image URL. Run `Upload asset from URL` first to get one for an image in your table.
    -   **Chart and sheet fields:** Tabular data as JSON, such as a list of row objects like `[{"Region":"APAC","Sales":10.2}]` or a list of rows whose first row holds the column names. A chart field takes up to 100 rows and 20 columns.

Optional:

-   **Design title:** A title for the new design, up to 255 characters. Defaults to the brand template's title.

**Outputs**

-   **Design ID:** The new design's Canva ID, ready to map into `Export design`.
-   **Design title:** The new design's title.
-   **Edit URL:** A link that opens the design in the Canva editor.
-   **View URL:** A link to view the design.

Each run creates a new design in the connected Canva account, so running a row again gives it a second design rather than updating the first.

### `Action` Upload asset from URL

Upload an image or video to the connected Canva account from a link in your table, and get back its asset ID.

**Inputs**

Required:

-   **File URL:** A public link to the image or video, such as a company logo or product shot. Canva downloads the file from this link, so it has to open without signing in.

Optional:

-   **Asset name:** A name for the asset in Canva. Defaults to the file name in the URL.

**Outputs**

-   **Asset ID:** The asset's Canva ID, such as `Msd59349ff`. Map it into an image field in `Autofill brand template`.
-   **Asset type:** The kind of asset Canva created, such as an image or a video.
-   **Asset name:** The asset's name in Canva.
-   **Thumbnail URL:** A link to a thumbnail of the asset.

### `Action` Export design

Export a Canva design as a file and get a link to download it.

**Inputs**

Required:

-   **Design ID:** The ID of the design to export, such as `DAFVztcvd9z`.
-   **File format:** The type of file to export. Defaults to `pdf`.
    -   Documents and slides: `pdf`, `pptx`
    -   Images: `jpg`, `png`, `gif`
    -   Video: `mp4`
    -   Data: `csv`
    -   HTML: `html_bundle`, `html_standalone`, which export a single page

Optional:

-   **Pages:** Which pages to export, such as `1, 3-5`. Leave it empty to export every page.
-   **JPG quality:** Compression quality from 1 to 100, used only for `jpg` exports. Defaults to 90.
-   **Video quality:** The resolution for `mp4` exports, horizontal or vertical at 480p, 720p, 1080p, or 4K, such as `vertical_1080p`. Defaults to `horizontal_1080p`.

**Outputs**

-   **Download URL:** A link to the exported file. It stops working 24 hours after the export finishes, so save the file itself rather than the link. If the export produces more than one file, this links to the first.
-   **Number of files:** How many files the export produced.
-   **Download expires at:** When the download link stops working.

### `Action` Get design

Look up a Canva design's details by its ID.

**Inputs**

Required:

-   **Design ID:** The ID of the design to look up, such as `DAFVztcvd9z`.

**Outputs**

-   **Design title:** The design's title.
-   **View URL:** A link to view the design.
-   **Edit URL:** A link that opens the design in the Canva editor.
-   **Thumbnail URL:** A link to the design's thumbnail image.
-   **Page count:** How many pages the design has.
-   **Owner user ID:** The Canva ID of the user who owns the design.
-   **Owner team ID:** The Canva ID of the owner's team.
-   **Created at:** When the design was created.
-   **Updated at:** When the design was last updated.

If the design has been deleted or the connected Canva account can't access it, the action returns no data.

### `Action` Get design analytics

Get the view counts and viewing time for a Canva design.

**Inputs**

Required:

-   **Design ID:** The ID of the design to report on, such as `DAFVztcvd9z`.

**Outputs**

-   **Total views:** The design's total view count.
-   **Unique viewers:** How many different people viewed the design.
-   **Average view duration (seconds):** How long a view lasts on average.
-   **Total view duration (seconds):** The combined viewing time across all views.

As with `Get design`, a design the connected account can't access returns no data. A design no one has viewed yet returns 0 for each count. Both actions are refunded when they return no data, so a lookup that finds nothing doesn't cost you anything.

### **Run settings**

-   **Auto-update:** Recommended for `Autofill brand template` so that new rows added to your table get a design automatically.
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

## **FAQs**

### Why do large Canva runs take a while to finish?

Clay paces Canva runs for each connected Canva account, and runs over the limit wait their turn, so a large table can take a while to finish. `Export design` runs up to 20 times a minute per account, and `Upload asset from URL` up to 30.

### What happens if I edit a brand template in Canva?

Re-select it in `Brand template` to load its current fields. Until you do, mapped fields that are no longer on the template are skipped, and a run fails if none of its mapped fields remain.

### What happens when I run the Canva source again?

By default, designs already in the table are skipped, so only new designs are added. To refresh details such as titles and page counts on existing rows, run `Get design` on the `Design ID` column.
