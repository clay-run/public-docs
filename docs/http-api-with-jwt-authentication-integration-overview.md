---
title: HTTP API with JWT authentication
source_url: https://university.clay.com/docs/http-api-with-jwt-authentication-integration-overview
description: Use HTTP API connections authenticated securely with JWT tokens.
last_synced: 2026-04-26T01:40:09.039Z
upstream_hash: baf5fda9deebdb1ed4a50be69c5cc749a9601122c44340559151b7c45f5b7b8b
---

# HTTP API with JWT authentication

Use HTTP API connections authenticated securely with JWT tokens.

The **HTTP API with JWT Authentication** action connects Clay to APIs that issue short-lived JWT tokens as part of their authentication flow. Before making API calls, Clay authenticates to your provider's token endpoint using stored credentials, then automatically injects the resulting JWT into each request's authorization header.

**Note:** For general information on HTTP methods, endpoint setup, request bodies, and response handling, see the [HTTP API guide](https://university.clay.com/docs/http-api-integration-overview).

## What is JWT authentication?

JWT (JSON Web Token) authentication is a two-step process:

1.  **Token fetch** — Clay calls your API's token endpoint (e.g., `https://api.example.com/oauth/token`) using the username and password stored in your JWT account, and receives a JWT in response.
2.  **Authenticated request** — Clay attaches the JWT as a header (e.g., `Authorization: Bearer <token>`) on every API call made by the enrichment.

The token is automatically refreshed approximately every 55 minutes, so you don't need to manage token expiry manually.

## How JWT authentication differs from standard HTTP API

Use this table to decide which action to use:

|  | HTTP API | HTTP API with JWT Authentication |
| --- | --- | --- |
| Auth flow | Direct — pre-stored headers sent with every request | Two-step — token fetch, then API call |
| Account required? | Optional | Required |
| What the account stores | Header key-value pairs (e.g., API keys, permanent bearer tokens) | Username, password, and token endpoint URL |
| Token expiry handled? | N/A | Auto-refreshed every ~55 minutes |

Use **standard HTTP API** when the API accepts static credentials (an API key, a permanent bearer token). Use **HTTP API with JWT Authentication** when the API issues a dynamically generated JWT — common in enterprise APIs like Gong and [Snov.io](http://Snov.io).

## Setting up your JWT account

Before adding the enrichment, you'll need to connect a JWT account to store your credentials at the workspace level. This account can be reused across any enrichment column that calls the same API.

**Note:** Have your API provider's authentication documentation open before completing these steps. You'll need the token endpoint URL and the correct format for credentials (some APIs use `client_id` and `client_secret` rather than traditional username/password).

1.  Navigate to `Settings` → `Connections`.
2.  Search for and select `HTTP API JWT Auth`.
3.  Click `+ Add account`.
4.  Enter the following details:
    -   `Username` — your API username or client ID.
    -   `Password` — your API password or client secret.
    -   `JWT Token Endpoint` — the URL Clay will call to obtain the JWT (e.g., `https://api.example.com/oauth/token`).
5.  Give the account a recognizable name (e.g., `Gong JWT`) and click `Save`.

## Enriching data with HTTP API with JWT Authentication

1.  Open your Clay table.
2.  Click `Add enrichment`.
3.  Search for and select `HTTP API with JWT Authentication`.
4.  In the `Account` dropdown, select your saved JWT account.
    -   If you haven't connected one yet, click `+ Add account` and complete the steps above.
5.  Configure the JWT-specific inputs (see below), then fill in the standard HTTP request fields for your API call.

### `Action` HTTP API with JWT Authentication

Sends HTTP requests authenticated with a dynamically fetched JWT token to any API endpoint.

**JWT auth fields — Required:**

-   `Location of JWT token in auth response` — The key name (using dot-notation) that identifies where the JWT appears in the token endpoint's JSON response. For example: `access_token`, `jwt`, or `data.token`. Check your API's documentation or test the token endpoint directly to confirm the exact path.

**JWT auth fields — Optional:**

-   `Token type` — The prefix added before the token value in the authorization header. Defaults to `Bearer`. Change this only if the API expects a different token type prefix (e.g., `Token`).
-   `Auth header name` — The name of the HTTP header Clay sets on each API request. Defaults to `Authorization`. Change this only if the API expects a non-standard header name (e.g., `X-Auth-Token`).

**Standard HTTP request fields:**

For all remaining request configuration — HTTP method, endpoint URL, query parameters, request body, headers, response filtering, retry settings, and redirect handling — see the [**HTTP API guide**](https://university.clay.com/docs/http-api-integration-overview). All options work identically between the two actions.

### Run settings

-   `Auto-update` — Re-runs the enrichment automatically when a referenced column value changes. Enable this if you're mapping dynamic values (such as a record ID) into the endpoint URL or request body.
-   `Only run if` — Add a conditional formula to skip rows that don't meet a specified condition. See [**conditional formulas**](https://university.clay.com/docs/formulas).

## FAQs

### How is this different from standard HTTP API?

Standard HTTP API attaches static, pre-stored headers (like an API key or a permanent bearer token) directly to each request. HTTP API with JWT Authentication first calls your API's token endpoint to obtain a fresh JWT, then uses that JWT for requests. This two-step flow is required by APIs that use short-lived tokens as part of their security model.

### When does my JWT token refresh?

Clay automatically refreshes the token approximately every 55 minutes. No manual action is needed when a token expires.

### What if the token is nested inside the response JSON?

Use dot-notation in the `Location of JWT token in auth response` field. For example, if the token endpoint returns `{"data": {"access_token": "eyJ..."}}`, enter `data.access_token`.

### Do I need a separate JWT account for each API I connect to?

Yes — each API has its own token endpoint and credentials, so a separate account is needed per API. Once created, however, an account can be reused across multiple enrichment columns within your workspace without re-entering credentials.

### What if I update my JWT account credentials?

Editing a saved JWT account will affect every enrichment column across your workspace that uses it. If you update the token endpoint or credentials, rerun any affected columns to confirm they're still returning results.

### What happens if I enter the wrong token location?

The enrichment will fail with the message `Please fill out your auth fields.` If you see this error, double-check the `Location of JWT token in auth response` field against the actual JSON structure returned by your token endpoint.
