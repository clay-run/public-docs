---
title: Troubleshoot Apollo API key and scope errors
description: Fix Apollo connection failures in Clay caused by missing API key
  scopes, including the endpoint and required key scope for each Apollo integration.
---

# Troubleshoot Apollo API key and scope errors

Fix Apollo connection failures in Clay caused by missing API key scopes, including the endpoint and required key scope for each Apollo integration.

## How the Apollo connection works

Clay's current Apollo integration is **OAuth-based**. When you connect Apollo, Clay authenticates each request with an OAuth access token — you do not paste or manage an Apollo API key, and you don't select scopes yourself. For a new (OAuth) connection, a "wrong API key scope" is not something you configure.

Some older Apollo columns use a **legacy API-key connection** that predates OAuth. These authenticate with a single Apollo API key sent as an `x-api-key` header, and the key's scope matters (see below). New connections use OAuth by default. To move off a legacy key, go to `Settings` → `Connections` → `Add connection` and search for **Apollo**.

## How Apollo API key scopes work

An Apollo API key is one of two types:

-   **Scoped key (default):** You pick the specific endpoints the key can access, and it only works for those. If a key calls an endpoint it wasn't granted, Apollo returns a **`403`** error such as:
    > This API key is not authorized to access `api/v1/mixed_people/api_search`. Request an API key from your administrator that includes this endpoint in its configured scope.
-   **Master key:** A master key grants access to every endpoint, so it satisfies all of the scopes below at once. Treat it like a password.

Every integration below works with **either** its listed scoped endpoint **or** a Master API key.

## Endpoint and required scope per integration

All endpoints share the base URL `https://api.apollo.io/api/v1/`.

| Clay integration | Apollo endpoint called | Required API key scope (or Master key) |
|---|---|---|
| Enrich Person | `people/match` | `api/v1/people/match` |
| Enrich Company | `organizations/enrich` | `api/v1/organizations/enrich` |
| Find People from Apollo (source) | `mixed_people/api_search` | `api/v1/mixed_people/api_search` |
| Find People at Company by Job Title | `mixed_people/api_search` | `api/v1/mixed_people/api_search` |
| Find Open Jobs | `organizations/{id}/job_postings` | `api/v1/organizations/job_postings` |
| Find Account by ID | `accounts/{id}` | `api/v1/accounts/show` |
| Find Contact by ID | `contacts/{id}` | `api/v1/contacts/show` |
| Find Saved Contacts | `contacts/search` | `api/v1/contacts/search` |
| Find or Create Contact | `contacts` | `api/v1/contacts/create` |
| Update Contact | `contacts/{id}` | `api/v1/contacts/update` |
| Add Contact to Sequence | `emailer_campaigns/{id}/add_contact_ids` | `api/v1/emailer_campaigns/add_contact_ids` |
| Update Contact Status in Sequence | `emailer_campaigns/remove_or_stop_contact_ids` | `api/v1/emailer_campaigns/remove_or_stop_contact_ids` |

**Note on scope names:** Apollo's scope string is a canonical action name and doesn't always match the literal URL path. For example, *Find or Create Contact* posts to `contacts` but the scope is `api/v1/contacts/create`, and *Add Contact to Sequence* posts to `emailer_campaigns/{id}/add_contact_ids` but the scope is `api/v1/emailer_campaigns/add_contact_ids`. When configuring a scoped key, grant the **scope** string, not the URL.

None of the integrations above require a master key — each works with a correctly scoped key.

## Fix a scope or 403 error

If a specific integration fails with a `403` or a "not authorized to access…" error:

1.  **Read the endpoint in the error message.** It names the exact scope that's missing.
2.  **Add that scope to your key.** In Apollo, go to `Settings` → `Integrations` → `API Keys`, edit your key, and add that endpoint to the key's scope — or enable **Set as master key** to cover everything at once.
3.  **Update the key in Clay** under `Settings` → `Connections`, then re-run the affected rows.

If you don't want to manage per-integration scopes, use a **Master API Key**. It grants access to every endpoint and eliminates scope-mismatch `403` errors.

## Other common API key errors

-   **"Invalid Apollo API key. Please check the key and try again."** — The key is incorrect or incomplete. Copy it fresh from Apollo (`Settings` → `Integrations` → `API Keys`) and re-enter it in Clay. Even a single missing character triggers this error.
-   **"Could not verify the Apollo API key. Please try again later."** — A temporary validation or network error, not a problem with the key itself. Re-run the affected rows.

## Integrations supported on legacy API-key connections

The legacy API-key connection supports only these integrations: Enrich Person, Enrich Company, Find People, Find People at Company by Job Title, Find Open Jobs, Find Account by ID, and Find Contact by ID. On this connection the people-search endpoint is `mixed_people/search` (without `api_`).

Find or Create Contact, Update Contact, Find Saved Contacts, and all Sequence actions are available only on the OAuth integration and cannot be reached with a user-supplied API key.

## Related

-   [Apollo.io integration](apollo-io-integration-overview.md)
