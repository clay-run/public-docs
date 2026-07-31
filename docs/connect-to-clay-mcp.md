---
title: Connect your platform to Clay MCP
description: Register your platform as an OAuth client and connect it to Clay's MCP server using Dynamic Client Registration.
last_synced: 2026-07-31T17:27:53.901Z
---

# Connect your platform to Clay MCP

Register your platform as an OAuth client and connect it to Clay's MCP server.

Clay exposes a [Model Context Protocol](https://modelcontextprotocol.io/) (MCP) server that lets an external platform — an AI assistant, IDE, agent host, or partner product — run Clay's find-and-enrich tools and custom functions on behalf of a signed-in Clay user. Dynamic Client Registration (DCR) is the self-service path onto that server: your platform registers itself at connect time to obtain OAuth client credentials, with no manual setup on Clay's side.

## How your platform discovers Clay

Clay advertises its OAuth endpoints through standard metadata documents, so a compliant client can find everything it needs starting from a single unauthenticated request.

**1.** Make an unauthenticated `POST` to `https://api.clay.com/v3/mcp`.

**2.** Clay responds `401 Unauthorized` with a `WWW-Authenticate` header pointing at the protected-resource metadata:

`WWW-Authenticate: Bearer resource_metadata="<https://api.clay.com/.well-known/oauth-protected-resource/v3/mcp>"   `

**3.** Fetch that document to learn the resource and its authorization server:

`{    "resource": "<https://api.clay.com/v3/mcp>",    "issuer": "<https://api.clay.com>",    "authorization_servers": ["<https://api.clay.com>"],    "scopes_supported": ["mcp"]   }   `

**4.** Fetch the authorization-server metadata at `https://api.clay.com/.well-known/oauth-authorization-server` to learn the OAuth endpoints:

`{    "issuer": "<https://api.clay.com>",    "authorization_endpoint": "<https://app.clay.com/oauth/authorize>",    "device_authorization_endpoint": "<https://api.clay.com/oauth/device_authorization>",    "token_endpoint": "<https://api.clay.com/oauth/token>",    "registration_endpoint": "<https://api.clay.com/oauth/register>",    "revocation_endpoint": "<https://api.clay.com/oauth/revoke>",    "scopes_supported": ["mcp"],    "response_types_supported": ["code"],    "grant_types_supported": [      "authorization_code",      "refresh_token",      "urn:ietf:params:oauth:grant-type:device_code"    ],    "token_endpoint_auth_methods_supported": ["client_secret_post", "client_secret_basic", "none"],    "revocation_endpoint_auth_methods_supported": ["client_secret_post", "client_secret_basic", "none"],    "code_challenge_methods_supported": ["S256"]   }   `

## Registering a client

Send a `POST` to the registration endpoint, following [RFC 7591](https://datatracker.ietf.org/doc/html/rfc7591). Registration is open — there is no Clay-side approval step.

### Choosing a client type

Pick the type by whether your client can keep a secret. PKCE is mandatory either way.

-   **Confidential** — the client holds a `client_secret`. Use this whenever the client runs on a server or backend you control, which covers most cloud-hosted platforms. Set `token_endpoint_auth_method` to `client_secret_basic` or `client_secret_post`.
-   **Public (PKCE-only)** — set `token_endpoint_auth_method` to `none` and expect no secret in the response. Use this only when the client runs on the end user's machine and cannot safely store a secret: installed and native apps, desktop clients, and CLIs. A secret bundled into a distributed app isn't secret, so these clients rely on PKCE alone.

### Registration request

`POST <https://api.clay.com/oauth/register>   Content-Type: application/json      {    "client_name": "Acme Assistant",    "redirect_uris": ["<https://acme.example.com/oauth/callback>"],    "grant_types": ["authorization_code", "refresh_token"],    "token_endpoint_auth_method": "client_secret_basic",    "scope": "mcp"   }   `

**Required:**

-   redirect\_uris: Array of at least one callback URL, each meeting the requirements below.

**Optional:**

-   client\_name: Display name shown to the user on Clay's consent screen, up to 128 characters.
-   grant\_types: Defaults to `["authorization_code"]`. Only `authorization_code` and `refresh_token` can be registered — include `refresh_token` if you want access that outlives a single token.
-   token\_endpoint\_auth\_method: One of `client_secret_basic`, `client_secret_post`, or `none`.
-   scope: Space-separated scopes. `mcp` is the only scope available to publicly registered clients.

Clay responds `201 Created`:

`{    "client_id": "cci_...",    "client_secret": "ccs_...",    "client_id_issued_at": 1769904000,    "client_secret_expires_at": 0,    "redirect_uris": ["<https://acme.example.com/oauth/callback>"],    "grant_types": ["authorization_code", "refresh_token"],    "token_endpoint_auth_method": "client_secret_basic",    "scope": "mcp"   }   `

The `client_secret` is returned only in this response, so store it before you discard the payload. A `client_secret_expires_at` of `0` means the secret does not expire. Public clients receive no `client_secret` field at all.

### Redirect URI requirements

Clay validates every entry in `redirect_uris` at registration:

-   Must use `https`, with two exceptions for native apps under [RFC 8252](https://datatracker.ietf.org/doc/html/rfc8252): loopback HTTP (`http://localhost`, `http://127.0.0.1`, or `http://[::1]`) and private-use schemes such as `acme://callback`.
-   Must not contain a username or password.
-   Must not contain a fragment.

At token exchange, the `redirect_uri` you send has to match the one the authorization code was issued against exactly.

## Authorizing and connecting

Once registered, run the standard authorization-code + PKCE flow.

1.  Open `https://app.clay.com/oauth/authorize` in the user's browser with your `client_id`, `redirect_uri`, `response_type=code`, `scope=mcp`, `code_challenge`, and `code_challenge_method=S256`.
2.  The user signs in to Clay, reviews the consent screen, and selects which of their workspaces to connect.
3.  Clay redirects back to your `redirect_uri` with a `code`, valid for five minutes.
4.  Exchange the code for tokens.

### Token exchange

`POST <https://api.clay.com/oauth/token>   Content-Type: application/x-www-form-urlencoded   Authorization: Basic base64(client_id:client_secret)      grant_type=authorization_code&code=<code>&redirect_uri=<redirect_uri>&code_verifier=<verifier>   `

Your `code_verifier` must be between 43 and 128 characters.

`{    "access_token": "...",    "refresh_token": "...",    "token_type": "Bearer",    "expires_in": 3600,    "scope": "mcp"   }   `

Access tokens last one hour. Refresh an expired token with `grant_type=refresh_token` at the same endpoint, authenticating the same way you do for the code exchange.

Clay rotates refresh tokens. Every refresh returns a new `refresh_token` alongside the new `access_token`, and the token you sent is retired — persist the new one each time, or the next refresh fails with `invalid_grant`. Presenting a refresh token under a different `client_id` than the one it was issued to revokes that token immediately, so don't reuse tokens across registrations.

### Connecting to the MCP server

1.  `POST` to `https://api.clay.com/v3/mcp` with an `Authorization: Bearer <access_token>` header.
2.  Make `initialize` your first call. Clay returns a session id in the `Mcp-Session-Id` response header.
3.  Send that `Mcp-Session-Id` header on every subsequent call, including `tools/list` and `tools/call`.

## Workspace requirements

Two things on the customer's side decide whether your client can connect at all.

First, the person authorizing has to be a member of the workspace they select, since tools run against that workspace's data.

Second, admins choose which clients their workspace accepts. Under `Allowed MCP clients` on the `MCP users` settings page, each client Clay recognizes gets its own toggle, alongside an `Unknown` option described in-product as `Use this for any other MCP client not listed above.` That `Unknown` toggle is the one that governs clients registered through DCR. Clay re-checks the policy every time it issues a token, so turning it off blocks token refreshes as well as new connections.

For how admins manage MCP access, credit limits, and functions, see [**MCP in Clay**](https://university.clay.com/docs/mcp-settings).

## Reference: endpoints

**PurposeProduction URL**MCP endpoint`https://api.clay.com/v3/mcp`OAuth issuer / authorization server`https://api.clay.com`Authorization server metadata`https://api.clay.com/.well-known/oauth-authorization-server`Protected resource metadata`https://api.clay.com/.well-known/oauth-protected-resource/v3/mcp`Authorization endpoint (user's browser)`https://app.clay.com/oauth/authorize`Token endpoint`https://api.clay.com/oauth/token`Registration endpoint (DCR)`https://api.clay.com/oauth/register`Revocation endpoint`https://api.clay.com/oauth/revoke`

## Troubleshooting

### Registration returns `429 too_many_requests`

Registration is rate-limited per IP address for publicly registered clients, with a burst of four requests and ten refilling per hour. The response carries a `Retry-After` header. Registration is meant to be a once-per-install action, so cache the credentials you receive instead of registering again for each connection.

### Registration returns `invalid_client_metadata`

A submitted field failed validation, and the `error_description` names the field and the reason. The usual causes are a `redirect_uris` entry that doesn't meet the requirements above, or a `grant_types` array containing something other than `authorization_code` and `refresh_token`.

### Authorization or refresh returns `access_denied`

When the description reads `This application is not permitted by your workspace policy`, an admin in the selected workspace has your client turned off under `Allowed MCP clients`. Because Clay re-checks the policy at token issuance rather than only at consent, this can surface on a refresh for a connection that worked previously.

### MCP calls fail with `Missing Mcp-Session-Id header`

Your client isn't sending the session id from `initialize`. Read the `Mcp-Session-Id` response header on the `initialize` call and attach it to every request in that session.

## FAQs

### Do I register once, or once per customer?

Once. A single registration serves every Clay user who connects through your platform — each user runs the authorization flow themselves and picks their own workspace at consent.

### Why does my application show as unverified on the consent screen?

Because registration is open, Clay can't treat a self-chosen `client_name` as an identity claim, so every publicly registered client is presented as an `Unverified application` and the consent screen shows the user your redirect destination. Clay marks a client as verified only when it recognizes that client independently of what the client calls itself, which is not something self-registration can establish.

### Can I use the device authorization flow instead?

Not through DCR. Clay advertises a `device_authorization_endpoint` and its token endpoint accepts the device code grant, but registration only accepts `authorization_code` and `refresh_token` as grant types. Use the authorization-code flow, and reach out to the Clay team if the device flow is genuinely the only option for your client.

### How long does a session last?

A session id from `initialize` stays valid for 14 days of inactivity, and each call you make on it extends that window. If a call returns `Session not found or expired`, call `initialize` again to start a fresh session rather than retrying with the old id.

### Does running tools through my platform cost the user extra?

No. Tools consume the connected workspace's credits at the same rate as the equivalent work done inside Clay — there is no surcharge for arriving over MCP. Admins can cap how many credits each user spends through an external platform.

### How do I disconnect a user?

`POST` the user's token to the revocation endpoint with your client credentials, following [RFC 7009](https://datatracker.ietf.org/doc/html/rfc7009). It accepts the same authentication methods as the token endpoint, including a bare `client_id` for public clients.
