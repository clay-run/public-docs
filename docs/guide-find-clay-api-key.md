---
title: Find your Clay API key
description: Utilize your Clay-native enrichments with your personal key.
last_synced: 2026-04-26T01:40:06.072Z
---

# Find your Clay API key

Utilize your Clay-native enrichments with your personal key.

A Clay API key is required for all Clay-native integrations.

To get started, you'll need a Clay account and your API key.

Your Clay API key enables you to:

-   Look up a single row in another table
-   Look up multiple rows in another table

### Find your Clay API key

1.  In the top bar, click your account name and select `Settings`
2.  Under `Account`, locate `API key`. You'll find your API key here for integrations.

### Using your API key with external tools

This personal API key is designed for use **within Clay** — specifically for Clay-native integrations such as cross-table lookups. It is not supported for use with external CLI tools, custom MCP clients, or direct REST API calls made from outside of Clay. If you attempt to use it in those contexts, you will receive an authentication error; this is expected behavior.

If you need programmatic access to Clay from an external tool or CLI, Clay offers a Public HTTP API (`api.clay.com`) that uses a separate workspace-scoped API key — this is distinct from the personal key described above. The Public HTTP API is currently in beta. To request access for your workspace, contact Clay support.