---
title: Google Slides integration
source_url: https://university.clay.com/docs/google-slides-integration
description: Create customized presentations at scale using your table data.
last_synced: 2026-04-26T01:40:05.093Z
upstream_hash: 3e74a287138a9214818ad28e18e8ab0fff893a63e9d586be3d0b715bd66994a4
---

# Google Slides integration

Create customized presentations at scale using your table data.

Clay's Google Slides integration lets you create customized presentations at scale using your table data. Build one smart template and generate hundreds of personalized decks in minutes—perfect for sales materials, QBRs, client updates, and more.

## **How it works**

The Google Slides integration uses a template-based approach to create personalized presentations:

1.  **Create a template** in Google Slides with variables (placeholders) in double curly brackets like `{{company_name}}` or `{{revenue}}`
2.  **Connect the integration** in Clay and select your template
3.  **Map your data** from Clay table columns to template variables
4.  **Generate presentations** automatically for each row in your table

Each presentation is saved as a new file in your Google Drive, dynamically filled with data from your Clay table.

## **Setting up the integration**

### **Connect your Google account**

1.  In a Clay table, click `Add enrichment` and search for `Google Slides`. Under `Integrations`, select `Create presentation`.
2.  In the modal, click `Select Google Slides account`:
    -   If you haven't connected Google Slides yet, click `+ Add account` and complete the authentication process.
    -   When adding your account, select your template presentation and click `Select files and folders` that Clay can access.

 **Tip:** Make sure to grant Clay access to both the template file and the folder where you want new presentations saved.

### **Create your template**

In Google Slides, create a presentation to use as your template. Add variables anywhere in your slides using double curly brackets:

**Examples:**

-   `{{company_name}}` → Company name from your table
-   `{{first_name}}` → Contact's first name
-   `{{custom_pitch}}` → Personalized pitch text
-   `{{company_logo-image}}` → Company logo (see image support below)

Variables can be placed in text boxes, headers, bullet points, or anywhere text appears in your slides.

### **Configure the enrichment**

**Inputs:**

**Template presentation**

Select the Google Slides file you want to use as your template.

**Google Drive folder** (Optional)

Choose where new presentations will be saved. If left empty, presentations are saved to your Google Drive root folder.

**Placeholders**

Map Clay table columns to the variables in your template. The integration automatically detects all variables from your template and creates input fields for each one.

### **Image support**

Google Slides supports dynamic images! Add images to your presentations by using variables that end in `-image`:

**Example:** `{{company_logo-image}}`

**Requirements:**

-   Image URLs must be publicly accessible
-   Images inherit the size of the text box containing the tag
-   Supported formats: JPG, PNG, GIF

**Note:** The Google Slides integration supports images! If you end your tag in `-image` (e.g., `company-logo-image`), the integration will replace your tag with the image. Image URLs must be publicly accessible, and images will take the size of the textbox that contains the tag.

### **Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

## **FAQs**

### **Can I use the same template for multiple tables?**

Yes! You can reuse templates across different tables. Just make sure the variable names in your template match the column names you want to map.

### **What happens if a variable has no value?**

If a Clay table cell is empty, the variable in the presentation will remain as the placeholder text (e.g., `{{company_name}}`). Use conditional formulas in the `Only run if` setting to prevent generating presentations with missing data.

### **Can I edit presentations after they're generated?**

Yes! Generated presentations are standard Google Slides files saved to your Drive. You can edit them manually after creation.

### **How many presentations can I generate at once?**

You can generate presentations for every row in your Clay table. For tables with thousands of rows, consider using filters or the `Only run if` setting to control which rows generate presentations.

### **Do images need to be hosted somewhere specific?**

Images must be publicly accessible via URL. You can use image URLs from company websites, uploaded files with public links, or image hosting services. Private or authentication-required URLs won't work.
