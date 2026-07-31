---
title: Audiences Security & Privacy
description: Covers how data enters Audiences, which permission types can access it, and how Clay stores, retains, and deletes workspace data.
last_synced: 2026-07-31T17:31:06.291Z
---

# Audiences Security & Privacy

How data enters Audiences, which permission types can reach it, and how Clay stores, retains, and deletes it.

Audiences is a persistent data layer — records imported from your CRM or data warehouse stay in Clay, accumulate enrichment and signal data over time, and can be written back out to connected systems. Because that data persists rather than passing through a single request, admins need to know who can reach it, what leaves the workspace, and how it is retained and removed.

**Note:** Two of the four permission types below are gated. `Viewer` is available on the Enterprise plan, and `Sales Rep` is in beta and enabled for select workspaces on request. If you don't see either one when inviting a team member, contact Clay support.

## How data enters Audiences

Every Audiences source is a workspace-level connection, not a per-user one. Once a source is connected, the records it imports are reachable by everyone with access to Audiences — access is governed by workspace permission type, not by who set the source up.

-   **Supported sources** are Salesforce, HubSpot, Snowflake, BigQuery, Databricks, CSV, and Clay's own people and companies database. Setup for each is covered in [Audiences](https://university.clay.com/docs/audiences).
-   **Enrichments and signals write permanently to records**, across every audience — not only the segment you ran them from. A field enriched once stays available as a filter everywhere in the workspace, so enriching a narrow segment still adds data to the shared layer.
-   **Records are resolved on ingestion.** Clay compares incoming records against its universal companies, people, and jobs dataset to tie first- and third-party data to a persistent identifier, and checks them against aliases already in your workspace. This runs automatically on every import and is not a per-audience setting.
-   **You choose the alias field for cross-source joins.** `Import record matching` controls which field — email or domain, for example — Clay uses to join a new source's records to records you already have. Configuration steps are in [Audiences](https://university.clay.com/docs/audiences).

## What each permission type can do in Audiences

A Clay workspace has four permission types, assigned from `Settings → Team`. Audiences enforces them as follows:

-   `Admin` — full access. Read data, create and delete audiences, connect and configure sources, configure CRM write-back, and manage enrichments, signals, actions, and fields.
-   `Editor` — everything an admin can do inside Audiences except connect a source or configure write-back. Those two are the paths that move data into and out of the workspace, which is why they are reserved for admins.
-   `Viewer` — read-only across Audiences data. This is all audience data in the workspace, not a subset you nominate.
-   `Sales Rep` — no Audiences access.

Permission types are workspace-wide. There is no per-audience access list, so a `Viewer` who should only see one segment cannot be restricted to it — scope access by deciding who joins the workspace at all. See [Roles and permissions](https://university.clay.com/docs/roles-and-permissions) for the full permission model and [User groups](https://university.clay.com/docs/user-groups) for managing assignments at scale.

## Controls available to admins

-   **Source connection is admin-only.** An `Editor` can build and enrich audiences but cannot point Clay at a new system of record.
-   **Field-level write-back control.** Every mapped field carries a `Scheduled export rule`: `Never write`, `Write if empty`, or `Always write`. The default is `Never write`, so Clay enriches a field in Audiences but sends nothing to your CRM until an admin changes that field's rule. This is the main lever for deciding what leaves the workspace.
-   **Record creation is separate from field updates.** `Create new Salesforce records` is off by default, so Clay updates records that already exist rather than creating new ones.
-   **Spend caps.** Workspace credit spend limits, and named [Credit budgets](https://university.clay.com/docs/credit-budgets) on Enterprise, cap what enrichment and signal runs can consume.
-   **Archive rather than delete.** Archived records leave your active audiences and stop matching filters, but stay browsable and restorable — useful when you need a record out of circulation without losing history.
-   **Single sign-on.** SSO is available on the Enterprise plan.
-   **Removing access.** Removing a user from the workspace is the definitive way to cut off their access to Audiences data.

## Shared responsibility

Clay secures the infrastructure, platform, and data processing layers. Your team controls what enters Audiences and where it goes.

**Clay's responsibilities:**

-   Maintain SOC 2 Type II certification, ISO 27001 compliance, and GDPR and CCPA compliance.
-   Encrypt data in transit and at rest.
-   Secure application code and infrastructure.
-   Vet and monitor third-party data providers and AI subprocessors.

The supporting documentation — the SOC 2 Type II report, the current AI subprocessor list, and security questionnaire responses — is available through the [Clay Trust Center](https://trust.clay.com), or by contacting [security@clay.com](mailto:security@clay.com).

**Your responsibilities:**

-   **Decide what to import** — Audiences syncs the objects and fields you map, not your whole CRM. Map the fields your team will actually segment and act on, and leave sensitive fields out of the mapping rather than importing them and restricting them later.
-   **Establish your lawful basis before importing** — you decide which records enter Audiences and what happens to them downstream, including any advertising or outreach use.
-   **Review write-back before enabling it** — leave fields on `Never write` until you have validated Clay's data quality against your own, so an export cannot overwrite actively maintained CRM data.
-   **Keep your permission assignments current** — because access is workspace-wide, offboarding in Clay matters as much as offboarding in your CRM.

## How Clay handles data in Audiences

-   **Your data is stored, not just passed through.** Unlike a single enrichment request, Audiences retains records for as long as the source stays connected, so that segmentation and enrichment can run continuously against them.
-   **Your data is never used for AI model training.** Clay holds contractual agreements with all of its AI providers that prohibit training on customer data.
-   **Your data is not shared with other customers.** Workspace data stays logically isolated.
-   **Data is encrypted in transit and at rest.** Clay uses TLS 1.2/1.3 for all data transmission and industry-standard encryption at rest.
-   **You can delete your data at any time.** Deleting a workspace removes all of its data after 30 days.

## Retention and deletion

What you can do yourself, and what needs Clay's help:

-   **Delete an audience** — an `Admin` or `Editor` can delete a segment. This removes the segment definition, not the underlying records, which stay in the shared data layer.
-   **Archive records** — the self-serve way to take specific records out of active use. Archived records are recoverable.
-   **Delete a workspace** — removes all workspace data after 30 days. See [Account and workspace settings](https://www.clay.com/university/guide/workspace-administration-documentation) for requirements and the exact steps.
-   **Purge specific records or a whole source's imported data** — not currently a self-serve action. Contact Clay support or your Growth Strategist, who can run a targeted deletion for named records, a segment's records, or the workspace's Audiences data.

## FAQs

### Can we see where a particular value came from?

Yes. Open any record's detail view and each field shows its originating source, so you can distinguish a value your CRM supplied from one Clay enriched or a signal produced. The `Fields` tab in the Data hub shows the same attribution at the field level, alongside fill rate and cost.

### If we turn off a source's import sync, does the data it already imported disappear?

No. Turning off `Import sync` stops new and changed records flowing in, but records already ingested stay in your audiences, keep their enriched fields, and continue matching filters. Removing that data is a separate deletion request.

### How do we handle an erasure request for one individual?

Delete or suppress them in your source system first, so the next sync does not reintroduce them, then archive the record in Audiences to take it out of active use. Because archiving is recoverable rather than a purge, follow up with Clay support for a hard deletion where your policy requires the record to be destroyed rather than deactivated.

### Does a `Viewer` who can see Audiences data also have a way to get it out?

Not through Audiences. Export paths — CRM write-back and the CSV download in the ad-sync flow — require write access, so they are unavailable to a `Viewer`. A `Viewer` can still read data on screen, which is worth weighing when you grant the permission type.

### Are records in Audiences automatically eligible for ad targeting?

No. Nothing syncs to an ad platform until someone creates an ad sync for a specific segment, and that surface applies its own restrictions — including excluding records outside the US that Clay's own dataset is the only source for. See [Clay Ads](https://university.clay.com/docs/clay-ads) and [Clay Ads compliance best practices](https://university.clay.com/docs/clay-ads-compliance-best-practices) before you sync.
