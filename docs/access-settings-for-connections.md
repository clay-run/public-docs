---
title: Access settings for connections
source_url: https://university.clay.com/docs/access-settings-for-connections
last_synced: 2026-04-26T01:39:38.272Z
upstream_hash: 1f7c0974ae32110d89b689f026ff4d2331ca87453049179d3d7a89b72782be70
---

# Access settings for connections

Determine who in the workspace is allowed to build with certain connections or MCP servers.

**Note:** This feature is for users on an Enterprise Plan.

Every connected account in Clay (e.g., Salesforce, OpenAI, Snowflake) has access controls, so you can determine who in the workspace is allowed to create workflows and columns with certain connections.

Admins and connected account owners can determine who in the workspace is allowed to build with certain connections or MCP servers by managing permissions in Settings. When building workflows or columns in Clay, users will only see connections they have access to. All users in the workspace can run workflows and columns that are already set up.

## Managing connections as an admin

Admins can control connection access in two ways: (1) setting permissions on existing connections to determine who can build workflows and columns with them; (2) requiring approval before members add new connections to the workspace.

### Requiring approval to add new connections

Admins can require that workspace members request approval before adding any new connection to the workspace. When enabled, this helps prevent unapproved tools from accessing workspace data.

**To enable:**

1.  Navigate to `Settings` → `Connections`.
2.  Toggle on `Require approval to add connections` in the connection settings panel.

**How it works:**

Once enabled, when a non-admin member tries to add a new connection to an external provider, they will see `Request access` instead of the standard add-connection flow. The member can include an optional reason for the request. The request is then sent to all workspace admins via email.

Admins will have seven days to **approve** or **deny** each request from the email notification. If approved:

-   The member can add **one connection** for the approved provider. The member will have seven days from the request being approved to do so.
-   To add another connection to the same provider, they must submit a new request.

### Setting permissions on a connection

1.  Navigate to `Settings` → `Connections`
2.  Find the connection you want to manage (e.g., OpenAI, Salesforce, HubSpot).
3.  Under access settings, choose one of the following options:
    -   `Anyone in the workspace` — All workspace members can configure columns or workflows with this connection
    -   `Specific people and groups` — Only admins and the people or user groups you name can configure workflows or columns with this connection
4.  If you selected `Specific people and groups`:
    -   Search for and add individual  members or user groups who should have access
    -   Add [user groups](https://university.clay.com/docs/user-groups) to grant access to all members of that group
    -   To remove access, simply remove individual members or groups from the allowlist.
5.  Click `Save` to apply the changes

To update access later, just edit the connection and add or remove users or user groups from the allowlist.

## What users can and cannot do

If a user does not have access to a connection, they can or cannot do the following across Clay:

**Not allowed ❌**

-   Configure a workflow or column using that connection
-   Edit existing column logic and mappings
-   Duplicate the column or rename it
-   Save it as a function (the function will be saved, but the connection will not be copied over — you'll need to select a connection you have access to)
-   Edit or reorder steps in a waterfall that uses that connection
-   Leverage that connection for Claygent context or AI snippets in campaigns

**Allowed ✅**

-   Run the column and view run info
-   View column logic in read-only mode
-   Swap the restricted connection to a different connection the user **does** have access to
-   Edit table data and build derived tables/columns (unless in view-only mode)

## Controls by feature

### Columns

If the column uses a connection the user doesn't have access to, users can see the column logic in read-only mode. They can swap the restricted connection for one they have access to. Once they do, the column becomes fully editable under their credentials.

### Waterfalls

A waterfall is a priority-ordered list of providers tried in sequence until one returns a usable result. A user's ability to edit a waterfall depends on how many of connections in the waterfall they're allowlisted for:

| Access level | Enable/disable providers | Edit provider settings | Reorder / add steps | Delete connections | Swap connections |
| --- | --- | --- | --- | --- | --- |
| No connection access | ❌ | ❌ | ❌ | ❌ | ✅ |
| Mixed connection access | ❌ | ❌ | ❌ | ❌ | ✅ |
| Full connection access | ✅ | ✅ | ✅ | ✅ | ✅ |

Regardless of access state, users can always view the full waterfall configuration (providers, order, selected connections) and swap in connections they're allowlisted for.

### Signals

Signals follow the same access rules as a single column:

-   The connection dropdown only shows connections the user is allowed to use.
-   If the user doesn't have access to the connection currently on the signal, the logic editor is read-only. They can swap in a connection they do have access to to unlock editing.

### Functions

-   When building a function, you can only leverage connections you're allowed to use
-   When **using** an existing function, any columns that leverage connections a user doesn’t have access to appear as read only. Users must swap in their own key to unlock edit functionality.
-   To prevent others from editing your function, use view-only permissions on the function itself until a more comprehensive permissions model is available.

### Claygent

-   When **creating** a Claygent, connection access controls apply when adding documents or connecting data sources.
-   When running an existing Claygent, users can only leverage connections they're allowlisted for. For example, if you run a Claygent, it will use your own OpenAI connection rather than another user's connection. Within the Claygent builder experience itself, no functionality is limited.

### Audiences, Sculptor, and Prospector

Enrichment columns within bulk enrichment tables (Audiences) and Sculptor/Prospector surfaces follow the same access rules described above for individual columns and waterfalls.

## FAQs

**Can admins access every connection in the workspace?**Admins do not, by default, have access to build workflows with every connection in the workspace. All admins can, however, add themselves to any connection in the workspace. Admins are always able to manage and view all connections in the workspace.

**What's the default for new keys?**

Admins and connection owners must explicitly add users or user groups to build workflows and columns with that key.

**Can a user still run a column that uses a connection they don't have access to?**

Yes. Controls are enforced at configuration time, not run time. Users can run existing columns and view run results even if they can't edit the underlying logic of a column.

**What if I want to use a different connection for my own work?**

You can swap the restricted connection out for any connection you're allowlisted for. This lets you run the same logic under your own credentials without changing it for others.

**What happens when an employee leaves the workspace?**

When a user is deactivated, their personal credentials are disabled by default.

**How do I set up controls for my workspace?**

Enterprise customers can configure allowlists independently or with the help of their Growth Strategist.
