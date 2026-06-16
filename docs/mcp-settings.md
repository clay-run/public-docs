---
title: MCP settings
source_url: https://university.clay.com/docs/mcp-settings
description: Connect your Clay workspace to AI tools.
last_synced: 2026-04-26T01:40:20.821Z
---

# MCP settings

Connect your Clay workspace to AI tools.

## Overview

Clay's MCP (Model Context Protocol) server lets you connect your Clay workspace directly to MCP-compatible AI tools like Claude, Cursor, Windsurf, and others. Once connected, you can interact with your Clay data through natural language and AI-powered workflows.

You can access MCP settings from **Settings → MCP settings**.

## Connecting Clay to Claude Desktop

To connect Clay to Claude Desktop:

1. Open **Settings** → **MCP settings** in Clay.
2. Copy the MCP server configuration shown.
3. Open your Claude Desktop configuration file and add the Clay MCP server configuration.
4. Restart Claude Desktop to apply the changes.

Detailed setup instructions are available in [Using Clay in Claude](using-clay-in-claude.md).

## Authentication and security

Clay's MCP server uses API key authentication. Your MCP API key:

-   Is generated when you set up the MCP connection.
-   Grants access to your Clay workspace data through the MCP server.
-   Should be kept secure and not shared.

To regenerate your MCP API key, go to **Settings → MCP settings** and click **Regenerate API key**. Note that regenerating the key will invalidate the previous key and require updating any existing MCP configurations.

## Permissions

The MCP server operates within the permissions of your Clay account. It can access:

-   Tables and workbooks you have access to.
-   Data you are authorized to view and modify.

## Supported MCP clients

Clay's MCP server is compatible with any MCP-compliant AI client, including:

-   Claude Desktop
-   Cursor
-   Windsurf
-   Other MCP-compatible tools

## Troubleshooting

If you encounter issues with the MCP connection:

-   Verify your API key is correctly configured in the client.
-   Ensure Clay's MCP server URL is correctly entered.
-   Check that your Clay account has the necessary permissions.
-   Try regenerating the API key if authentication fails.

For detailed setup guidance, see [Using Clay in Claude](using-clay-in-claude.md).
