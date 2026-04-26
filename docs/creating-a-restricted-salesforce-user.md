---
title: Creating a restricted Salesforce user
source_url: https://university.clay.com/docs/creating-a-restricted-salesforce-user
description: Create a restricted user with limited field-level access.
last_synced: 2026-04-26T01:39:48.438Z
upstream_hash: acd13fae2596557e96fd29cfd408198511092f9a5476d94de9df70dc5fc42b85
---

# Creating a restricted Salesforce user

Create a restricted user with limited field-level access.

When connecting Salesforce to Clay, you want to prevent accidental exposure of sensitive CRM data. By creating a restricted user with limited field-level access, you can safely enrich your data without giving Clay full visibility into your entire Salesforce org.

This restricted user can still write approved enrichment data back into Salesforce, without exposing your entire CRM.

Salesforce permissions work in 3 layers:

1.  **Object Permission**: Can you open the file cabinet?
2.  **Field Permission**: Can you see the papers inside?
3.  **Record Sharing**: Can you see every file cabinet?

We'll configure all three to ensure Clay has just the access it needs.

## **Create a custom permission set**

1.  In Salesforce, go to `Setup` → `Permission Sets` → `New`
2.  Enter these details:
    -   `Label`: Account Limited Read + Writeback
    -   `License`: Salesforce
3.  Click `Save`

## **Set object-level permissions**

1.  Within your new permission set, go to `Object Settings`
2.  Find and select `Account`
3.  Enable `Read` only
    -   If you plan to write enrichment data directly to Account fields, also enable `Edit`
    -   Otherwise, leave `Edit` disabled for maximum security

**Optional best practice**: Instead of editing Account directly, create a custom object like `Clay_Writeback__c` to store enriched data. This keeps your core CRM objects clean and auditable.

If you create a custom writeback object:

-   Grant `Read`, `Create`, and `Edit` on the custom object
-   Keep `Account` as `Read` only

## **Configure field-level security**

1.  Go to `Object Settings` → `Account` → `Field Permissions`
2.  Make these fields visible:
    -   `Account Name`
    -   `Domain` (or `Website` field)
    -   `Record ID`
    -   Any other limited fields you want Clay to access
3.  Hide all other `Account` fields

### **If writing directly to Account fields**

If you're writing enrichment data back to `Account` (rather than a custom object), grant `Edit` access to specific fields only:

-   `Clay_Status__c`
-   `Clay_Enriched__c`
-   `Clay_Last_Update__c`
-   Any other approved enrichment fields

Everything else should remain hidden.

## **Set system permissions**

1.  Within your permission set, go to `System Permissions`
2.  Enable:
    -   `API Enabled`
3.  Do NOT enable:
    -   `View All Data`
    -   `Modify All Data`
    -   `Customize Application`

## **Restrict record visibility (optional)**

If you only want Clay to see a subset of your `Accounts` (e.g., certain regions or segments), configure record-level sharing:

1.  Go to `Setup` → `Sharing Settings`
2.  Set `Accounts` organization-wide default to `Private`
3.  Create a sharing rule:
    -   Go to `Sharing Rules` for `Accounts`
    -   Click `New`
    -   Define criteria (e.g., `Region = EMEA`)
    -   Share with the integration user or their role

You can also use manual sharing or role-based access depending on your needs.

## **What this user can do**

The user you authenticate with Clay can now:

-   ✅ See only `Account Name`, `Domain`, and `Record ID`
-   ✅ Write back approved enrichment fields
-   ❌ View other `Account` fields
-   ❌ Access `Contacts`, `Opportunities`, `Leads`, etc.

## **Static IP addresses for allowlisting**

For additional security, you can allowlist these IP addresses in your Salesforce settings:

-   52.7.81.233
-   18.209.121.250
-   35.170.109.137
-   54.86.28.41

To add these, go to `Setup` → `Network Access` → `New` and enter each IP range.

## **FAQs**

### **Can I use an integration-only user license for this?**

Yes, but integration user licenses have some limitations with OAuth flows. If you run into authentication issues, try using a full Salesforce user license instead.

### **What if I need Clay to access multiple objects?**

Repeat the object-level and field-level security steps for each object you want to grant access to (e.g., Contacts, Leads). Always follow the principle of least privilege—only grant the minimum access needed.

### **How do I test that the restricted user is working correctly?**

Log in to Salesforce as the restricted user (or use "Login as" if you're an admin) and verify:

-   You can only see the fields you configured
-   Object access matches your permission set
-   Clay can successfully authenticate and pull data

### **Can I revoke access later?**

Yes. You can disable the permission set, delete it entirely, or disconnect the user from Clay at any time through `Setup` → `Permission Sets` or your Clay workspace settings.
