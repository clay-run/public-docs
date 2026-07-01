---
title: Apollo.io integration
description: AI-powered platform for sales intelligence, engagement, and
  workflow automation.
last_synced: 2026-04-27T18:09:15.331Z
---

# Apollo.io integration

AI-powered platform for sales intelligence, engagement, and workflow automation.

The Apollo and Clay integration enables users to find and enrich leads within Clay by leveraging [Apollo.io](http://Apollo.io)'s extensive B2B database.

## **Creating a table with** [**Apollo.io**](http://Apollo.io)

1.  In a workbook, click `+ Add` at the bottom.
2.  Search for [`Apollo.io`](http://Apollo.io) and select from the results.
3.  In the modal, you will be asked to `Select Apollo.io account`.
    -   If you haven't already connected your [Apollo.io](http://Apollo.io) account, click `+ Add account` and go through authentication.

### **`Source`** **Find People from Apollo**

Find people in [Apollo.io](http://Apollo.io) based on job titles and company domains.

**Inputs**

-   **Job Titles** (Required): Enter job titles to search for, separated by commas (e.g., `CEO, CTO, VP of Sales`)
-   **Company Domains** (Optional): Filter results to people at specific companies
-   **Limit** (Optional): Maximum number of people to return (1-1,000)

## **Setting up the** [**Apollo.io**](http://Apollo.io) **integration**

1.  While in a Clay table, click `Add enrichment` and search for [`Apollo.io`](http://Apollo.io).
2.  Under `Integrations`, select one of the [Apollo.io](http://Apollo.io) options.
3.  In the modal, you will be asked to `Select [Apollo.io](<http://Apollo.io>) account`.
    -   If you haven't already connected your [Apollo.io](http://Apollo.io) account, click `+ Add account` and go through authentication.

## **Using the** [**Apollo.io**](http://Apollo.io) **integration**

### **`Action`** **Enrich Person**

Retrieve additional data about an individual in [Apollo.io](http://Apollo.io) by providing identifying details.

**Inputs**

-   First Name (Optional): First name of the individual
-   Last Name (Optional): Last name of the individual
-   Name (Optional): Full name of the individual
-   Email Address (Optional): Email address of the individual
-   Company Name (Optional): Company where the individual works
-   Company Domain (Optional): Domain of the company
-   Apollo ID (Optional): Unique Apollo ID for the person

**Output:**

Returns comprehensive person details including:

-   Contact information (email, phone numbers)
-   Job title and employment history
-   Company and organization details
-   LinkedIn profile and social URLs
-   Department and seniority level
-   Location information

### **`Action`** **Enrich Company**

Enrich company data by providing a company domain, using [Apollo.io](http://Apollo.io)'s extensive database.

**Inputs**

-   **Company Domain**: The domain of the company to enrich (e.g., "[example.com](http://example.com)")

**Output:**

Returns detailed company information including:

-   Industry and company description
-   Employee count and departmental headcount
-   Annual revenue and financial data
-   Technologies used (tech stack)
-   Company headquarters and office locations
-   Social media profiles (LinkedIn, Facebook)
-   Founded year and company type

### **`Action`** **Find Open Jobs**

Retrieve open job postings for a company using [Apollo.io](http://Apollo.io)'s job database.

**Inputs**

-   Company ID (Optional): Apollo organization ID to identify the company
-   Job Search Terms (Optional): Keywords to filter job postings (comma-separated)

**Output:**

Returns:

-   **Job Postings** array containing:
    -   Job title
    -   Job posting URL
    -   Location (city, state, country)
    -   Posted date and last seen date
-   **Total Jobs Count**: Total number of open positions

### **`Action`** **Find Account by ID**

Use this action to retrieve detailed information for a specific account in [Apollo.io](http://Apollo.io) using an Account ID.

**Inputs**

-   **Apollo Account ID**: The unique Account ID in Apollo to search for

**Output:**

Returns comprehensive account information including:

-   Organization details (name, domain, industry)
-   Employee count and company size
-   Technologies and tech stack
-   Contact information
-   Office locations
-   Social profiles and website information

### **`Action`** **Find Contact by ID**

Retrieve detailed information about a specific contact in [Apollo.io](http://Apollo.io) by using a Contact ID.

**Inputs**

-   **Apollo Contact ID**: The unique Contact ID in Apollo to look up the contact

**Output:**

Returns detailed contact information including:

-   Full name and job title
-   Email addresses and phone numbers
-   Company and account details
-   LinkedIn profile and social URLs
-   Email verification status
-   Engagement history

### **`Action`** **Find People at Company By Job Title**

Use this action to search for individuals at specified companies by their job titles within [Apollo.io](http://Apollo.io).

**Inputs**

-   **Job Titles**: A comma-separated list of job titles to search for (e.g., "Marketing Manager, Sales Director")
-   **Company Domains**: A comma-separated list of company domains to filter the search (e.g., "[example.com](http://example.com)")
-   Locations (Optional): A comma-separated list of locations to further refine the search
-   Limit (Optional): Specify the maximum number of people to return in the search, up to 10
-   Include Contacts (Optional): Include relevant contacts from your linked CRM. If a limit is set, CRM contacts will be prioritized within the results

**Output:**

Returns a **Results** object containing:

-   **People** array with details for each person found:
    -   Name and contact information
    -   Job title and seniority
    -   Company and employment information
    -   LinkedIn profile
    -   Department and location
-   Contact verification status
-   Employment history

### **`Action`** **Find Saved Contacts**

Find saved contacts in your [Apollo.io](http://Apollo.io) account by searching with keywords.

**Inputs**

-   **Keywords**: Keywords to search by (recommended to use email address for best results). Keywords can also include combinations of names, job titles, and employers (company names)
-   Limit (Optional): Maximum number of contacts to return in the search (1-10)

**Output:**

Returns array of matching contacts including:

-   Contact information (name, email, phone numbers)
-   Job title and organization details
-   LinkedIn profile
-   Email verification status
-   Contact stage and owner information
-   Custom fields
-   Sequence enrollment status (if applicable)

### **`Action`** **Find or Create Contact**

Finds a contact in [Apollo.io](http://Apollo.io) or creates a new one if it doesn't exist.

**Inputs**

-   Run Dedupe (Optional, default: true): If enabled, Apollo will dedupe contacts by email address, LinkedIn URL, or name and organization name, returning existing contacts instead of creating duplicates
-   First Name (Optional): First name of contact
-   Last Name (Optional): Last name of contact
-   Email (Optional): Email address of contact
-   Job Title (Optional): Job title of contact
-   Organization Name (Optional): Name of organization contact belongs to
-   Website URL (Optional): Website URL of organization
-   Account ID (Optional): Apollo ID of organization contact belongs to
-   Direct Phone (Optional): Primary phone number for contact
-   Mobile Phone (Optional): Mobile phone number of contact
-   Present Raw Address (Optional): Personal location for contact (city, US state, country)
-   Contact Stage ID (Optional): Current stage of contact in sales process
-   Custom Fields (Optional): Custom fields defined in Apollo account settings

**Output:**

Returns contact object with:

-   Contact ID and basic information
-   Email verification status
-   Organization and location details
-   Custom field values
-   A flag indicating whether the contact was newly created or already existed (`was_existing`)

**Note:** This action intelligently finds existing contacts when deduplication is enabled, preventing duplicate records in your Apollo account.

### **`Action`** **Update Contact**

Updates an existing contact's information in [Apollo.io](http://Apollo.io).

**Inputs**

-   **Contact ID**: Apollo contact ID to update
-   First Name (Optional): First name of contact
-   Last Name (Optional): Last name of contact
-   Email (Optional): Email address of contact
-   Job Title (Optional): Job title of contact
-   Organization Name (Optional): Name of organization contact belongs to
-   Website URL (Optional): Website URL of organization
-   Account ID (Optional): Apollo ID of organization contact belongs to
-   Direct Phone (Optional): Primary phone number for contact
-   Mobile Phone (Optional): Mobile phone number of contact
-   Present Raw Address (Optional): Personal location for contact (city, US state, country)
-   Contact Stage ID (Optional): Current stage of contact in sales process
-   Custom Fields (Optional): Custom fields defined in Apollo account settings

**Output:**

Returns updated contact object with:

-   Complete contact information
-   Email verification status
-   Organization and location details
-   Updated custom field values
-   Metadata (owner, creator, timestamps)

**Note:** At least one optional field must be provided along with the Contact ID to perform an update.

### **`Action`** **Add Contact to Sequence**

Add a contact to a sequence in [Apollo.io](http://Apollo.io). The contact must already exist in [Apollo.io](http://Apollo.io).

**Inputs**

-   **Sequence ID**: ID of sequence to add contact to
-   **Contact ID**: ID of contact to add to sequence
-   **Send Email From Email Account ID**: ID of email account to send from
-   User ID (Optional): ID of user adding the contact to sequence
-   Add Without Email (Optional, default: false): Add contact to sequence without an email address?
-   Add Unverified Email (Optional, default: false): Add contact to sequence with unverified email address?
-   Add With Job Change (Optional, default: false): Add contact to sequence with a job change?
-   Add Active in Other Campaigns (Optional, default: false): Add contact to sequence if active in other campaigns?
-   Add Finished in Other Campaigns (Optional, default: false): Add contact to sequence if finished in other campaigns?

**Output:**

Returns confirmation of whether the contact was successfully added to the sequence, or if skipped, the reason for skipping (e.g., already in sequence, missing email, etc.)

**Note:** The optional override flags allow you to bypass common sequence enrollment restrictions.

### **`Action`** **Update Contact Status in Sequence**

Update the status of a contact in a sequence in [Apollo.io](http://Apollo.io). The contact must already exist in [Apollo.io](http://Apollo.io) and be enrolled in the sequence.

**Inputs**

-   **Sequence ID**: ID of sequence the contact is in
-   **Contact ID**: ID of contact to update in sequence
-   **Mode**: Action to take on the contact:
    -   **Remove from Sequence**: Permanently removes the contact from the sequence
    -   **Pause in Sequence**: Pauses the contact in the sequence (can be resumed later)
    -   **Mark as Finished**: Marks the contact as having completed the sequence

**Output:**

Returns confirmation of whether the contact's status was successfully updated, including details about the operation performed.

**Note:** Use this action to manage contact progression through your sequences, whether pausing outreach temporarily, removing contacts entirely, or marking campaigns as complete.

### **Run settings**

-   **Auto-update**
-   **Only run if**: The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.notion.so/source-S3-bucket-1417e66eb01481cc8a4cc485b14af577?pvs=21))

## Troubleshooting

### General API errors and import failures

If Apollo enrichments fail with unexpected errors — cells marked as errored without a clear credits, rate-limit, or configuration cause — try these steps in order:

1. **Hard-refresh the page** — press `Cmd+Shift+R` (Mac) or `Ctrl+Shift+R` (Windows/Linux) to clear stale browser state and reload the current run status.
2. **Re-run only the affected rows** — right-click any errored row and choose **Run [N] rows**, or open the enrichment column's run dropdown and select **Run [N] empty or out-of-date rows** to re-queue all errored and unrun cells in that column.
3. **Use Clay's native search as a temporary alternative** — Clay's built-in **Find People** and **Find Companies** sources draw from Clay's own data index and are not affected by Apollo API issues. You can use them to locate companies and people while the Apollo API is unavailable. For setup details, see [Finding companies and people in Clay](finding-companies-and-people-in-clay.md).

### Placeholder email addresses: `email_not_unlocked@domain.com`

When retrieving contacts via **Find People from Apollo**, the email field may contain `email_not_unlocked@domain.com` instead of a real address. Apollo only provides verified email addresses for contacts that have been unlocked using Apollo credits. If a contact hasn't been unlocked, Apollo returns this placeholder.

To resolve:

-   Use Apollo credits to unlock the contact in your Apollo account.
-   Use the **Enrich Person** action, which retrieves verified email addresses when sufficient identifying information is supplied.

### Insufficient credits

Apollo enrichments in Clay can consume either **Clay Data Credits** or **Apollo lead credits**, depending on which integration type is in use:

-   **Clay Data Credits**: Used with the current OAuth-based Apollo integration. New Apollo columns use OAuth by default.
-   **Apollo lead credits**: Used with older API-key-based Apollo columns. If you set up Apollo columns before the OAuth integration launched, those columns may still run against your own Apollo account's lead credits.

If an enrichment step fails with a credits error, first confirm which type of connection your column is using.

**If using the OAuth integration (Clay Data Credits):**

Check your Clay workspace credit balance. If credits are depleted, add more or upgrade your Clay plan.

**If using a legacy API-key-based Apollo column (Apollo lead credits):**

1.  Check your Apollo subscription to confirm it includes enough lead credits for the action. If not, upgrade through Apollo's settings.
2.  If you recently upgraded your Apollo account but still see the error in Clay, try reconnecting your Apollo account to refresh the connection. Ensure the credit type you have matches the activity you are performing.
3.  If Apollo credits are not recognized despite being available, there may be a brief delay in credit activation — try rerunning your rows after some time, or contact Apollo support.

### Null results in enrichment

The **Enrich Person** action requires both a person identifier and a company identifier to match successfully. Without a company identifier, fields like email, job title, and company details may return null.

To resolve, provide at least one company identifier alongside the person's name:

-   **Company Domain** (preferred)
-   Company Name

### Hitting Apollo's API rate limits with large row sets

Apollo enforces API rate limits that can cause cells to error when Clay processes a large list quickly. The available workaround depends on which column type you're using.

**Enrich Person and Enrich Company columns — use the Custom rate limit setting:**

1.  Open the column settings.
2.  Scroll to the **Custom rate limit** section.
3.  Set **Request Limit** (the maximum number of API calls allowed in the time window) and **Duration (in ms)** (the length of the window in milliseconds). For example: `Request Limit: 100, Duration: 60000` caps requests to 100 per minute.

**Action columns (Add Contact to Sequence, Find or Create Contact, and others) — run rows in manual batches:**

Action columns do not have a built-in rate limit control. To stay below Apollo's per-minute cap:

1.  Select a subset of rows (~150–200) by clicking the first row number and Shift-clicking the last.
2.  Right-click the selection and choose **Run [N] rows**.
3.  Wait approximately 60 seconds, then repeat for the next batch.

### Phone numbers returned are business lines, not personal mobile numbers

Apollo's database sources phone numbers from business directories, professional listings, and public records. Phone numbers returned by Apollo enrichments are typically direct dial numbers or business lines tied to a contact's work role — personal mobile numbers are rarely available, and when present tend to be for senior executives and US-based contacts.

To find personal mobile phone numbers, use a dedicated mobile phone waterfall. Clay's pre-built mobile phone waterfall (available under **Tools → Enrich → Phone number**) cascades through providers that aggregate personal mobile data from multiple sources. For provider recommendations and coverage by region, see [[Data test] Mobile phone providers by region](data-test-methodology-mobile-phone-region.md).

### Apollo API key connection errors

These errors appear on legacy Apollo columns that use an API key–based connection, set up before Clay's current OAuth integration launched.

-   **"Invalid Apollo API key. Please check the key and try again."** — The API key is incorrect or incomplete. Open your Apollo account settings, copy the API key, and re-enter it. Even a single missing character will trigger this error.
-   **"Could not verify the Apollo API key. Please try again later."** — This is a temporary network or server error during key validation, not a problem with the API key itself. Try running the affected rows again; the error typically resolves on retry.

To update your API key on an existing legacy Apollo connection, go to `Settings` → `Connections`, find your Apollo API key connection, and edit the credential.

**Note:** New Apollo connections use OAuth by default. If you need to add a new Apollo connection, go to `Settings` → `Connections`, click `Add connection`, and search for Apollo to set up the current OAuth-based integration.

## ‍