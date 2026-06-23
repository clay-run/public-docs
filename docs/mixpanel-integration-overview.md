---
title: Mixpanel integration overview
description: Product analytics platform.
last_synced: 2026-04-26T01:40:22.779Z
---

# Mixpanel integration overview

Product analytics platform.

## Mixpanel Overview

Mixpanel Cohorts are groups of users that share set of criteria. The Mixpanel Cohort Source allows you to export Cohorts of users into Clay based on project ID.

## Setting up the Mixpanel integration

Mixpanel connections require a **service account** (username and secret) — standard user email and password credentials may not reliably expose your projects. To create a service account, see [Mixpanel's service accounts documentation](https://developer.mixpanel.com/reference/service-accounts). Your service account username will end in `.mp-service-account`.

To set up the Mixpanel and Clay integration, follow these steps:

1.  Visit the Settings page and navigate to **Connections.**
2.  Click **\+ Add Connection** and select Mixpanel the menu.
3.  Enter your service account **username** (ending in `.mp-service-account`) and **secret**, then name your connection.

## Importing profiles from Mixpanel cohort as a source

1.  In a workbook, click `+ Add` at the bottom.
2.  Search for `Mixpanel` and select from the results.
3.  Add your account.
4.  Enter inputs for:
    -   Project ID
    -   Cohort Type

## Why a project doesn't appear in the Project ID list

Clay populates the **Project ID** dropdown by calling Mixpanel's API with the credentials of the selected connection. Only projects that the connected identity has been granted member access to in Mixpanel will appear — this is a Mixpanel-side permission, not a Clay setting.

If you have multiple connections and one shows more projects than another, it means the second identity hasn't been added as a member of those projects in Mixpanel.

**To fix missing projects:**
1.  In Mixpanel, open the project that isn't appearing.
2.  Go to **Project Settings → Access** and add the user or service account behind your Clay connection as a project member.
3.  Once the identity has access in Mixpanel, the project will appear in Clay.

If you need to start importing right away, switch your Clay source to the connection that already has access to the needed projects. For automated imports, using a dedicated service account is the most reliable long-term approach.
