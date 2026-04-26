---
title: Sendoso integration
source_url: https://university.clay.com/docs/sendoso-integration
last_synced: 2026-04-26T01:40:39.241Z
upstream_hash: 5ea2d30a6861cf791ba2c1b0ac024aa89de72c81209decfb7b6b47d170eb1623
---

# Sendoso integration

Enable personalized gift sending with AI-powered recommendations and approval workflows.

The Sendoso integration enables personalized gift sending with AI-powered recommendations and approval workflows, streamlining outreach through product suggestions and seamless tracking.

## **Enriching data with Sendoso**

1.  While in a Clay table, click `Actions` and search for `Sendoso`.
2.  Under `Integrations`, select one of the Sendoso options.

### **`Action` Send a gift recommended by Sendoso**

Send a recipient a gift personally recommended for them by Sendoso using their email, budget constraints, and shipping location. The gift will be sent once you approve it manually on the Sendoso platform.

## **Inputs**

-   **Recipient email (required):** The email address of the person receiving the gift.
-   **Recipient first name (required):** The first name of the person receiving the gift.
-   **Recipient last name (required):** The last name of the person receiving the gift.
-   **Maximum price (USD) (optional):** The maximum price in USD for the recommended product.
-   **Ship to country (optional):** Country where the gift will be shipped.
-   **Message (optional):** A custom message to include with the gift.
-   **Enable gift exchange (optional):** Allow the recipient to exchange the gift for another item of equal or lesser value. Defaults to `false`.
-   **Meeting URL (optional):** A URL to a meeting or calendar invite.

### **Important notes**

-   The action will return a status of `🟡 Pending approval` after successfully creating the send.
-   You must log into your Sendoso account to approve the gift before it will be sent to the recipient.
-   All sends created through this action require manual approval on the Sendoso platform.

### **Error messages**

-   **"Access token invalid. Please re-authorize with Sendoso":** Your Sendoso authentication has expired. Reconnect your Sendoso account.
-   **"Recipient email is required":** You must provide a recipient email address.
-   **"Please provide a valid recipient email address":** The email address format is invalid.
-   **"Recipient first name is required":** You must provide the recipient's first name.
-   **"Recipient last name is required":** You must provide the recipient's last name.
-   **"If providing a maximum price, please provide a valid maximum price in USD":** The price value must be a positive number.

### **`Action` Get gift recommendations**

Get personalized gift recommendations for a recipient based on their email address and preferences to discover suitable gifts during the research phase of your outreach campaigns.

## **Inputs**

-   **Recipient email (required):** The email address of the person you want to send a gift to.
-   **Maximum price (USD) (required):** Maximum price in USD for recommended gifts.
-   **Ship to country (optional):** Country where the gift will be shipped. Select from the dropdown list of available countries.

### **`Action` Send a gift of your choice**

Send a Sendoso gift of your choice to a recipient. The gift will be sent once you approve it manually on the Sendoso platform.

## **Inputs**

-   **Product variant ID:** The ID of the product variant to send. You can get this from the `Get Sendoso gift recommendations` action.
-   **Recipient email:** The email address of the person receiving the gift.
-   **Recipient first name:** The first name of the person receiving the gift.
-   **Recipient last name:** The last name of the person receiving the gift.
-   **Sender first name (Optional):** The first name of the person sending the gift.
-   **Sender last name (Optional):** The last name of the person sending the gift.
-   **Sender email (Optional):** The email address of the person sending the gift.
-   **Sender organization name (Optional):** The organization name of the person sending the gift.
-   **Message (Optional):** A custom message to include with the gift.
-   **Enable gift exchange (Optional):** Allow the recipient to exchange the gift for another item of equal or lesser value.
-   **Meeting URL (Optional):** A URL to a meeting or calendar invite.
