---
title: MCP Server
description: Learn how to connect an AI assistant to Marketo using the MCP server. Configure Claude Desktop, Cursor, Claude Code, or VS Code with your Marketo credentials.
hidefromtoc: true
exl-id: ab446e56-6250-4af5-b03e-162991d09a5c
---
# [!DNL Marketo] MCP Server

The Model Context Protocol (MCP) is an open standard that enables AI tools to communicate with external services. The [!DNL Marketo] MCP server acts as a bridge between your AI assistant and [!DNL Marketo]. It exposes more than 100 operations across forms, programs, smart campaigns, leads, emails, snippets, lists, and folders.

When your AI tool calls the MCP server, the server executes the corresponding REST API call on your behalf, using the credentials you provide in each request. You do not need to install, deploy, or run any server-side software.

## Prerequisites

- A [!DNL Marketo] instance with REST API access enabled
- Admin access to create API credentials in [!DNL Marketo] LaunchPoint
- One of the following AI tools: Claude Desktop, Cursor, Claude Code (CLI), or VS Code with GitHub Copilot
- Network access to the MCP server URL: `https://marketo-mcp.adobe.io/mcp`

## Get Marketo credentials

You need the following values from your [!DNL Marketo] instance:

- **Client ID**
- **Client Secret**
- **Munchkin Account ID**
- **REST API Endpoint**

If you already have them, skip to [Configure your AI tool](#configure-your-ai-tool).

### Client ID and Client Secret

1. Go to **[!UICONTROL Admin]** > **[!UICONTROL LaunchPoint]**.
1. Click your API service. If you do not have one, select **[!UICONTROL New]** > **[!UICONTROL New Service]**, choose **[!UICONTROL Custom]** as the service type, and assign a dedicated API user.
1. Click **[!UICONTROL View Details]** and copy the **[!UICONTROL Client ID]** and **[!UICONTROL Client Secret]** values.

### Munchkin Account ID

1. Go to **[!UICONTROL Admin]** > **[!UICONTROL Munchkin]**.
1. Copy the **[!UICONTROL Munchkin Account ID]**. The format is `XXX-XXX-XXX` and matches the prefix of your instance URL.

### REST API Endpoint

1. Go to **[!UICONTROL Admin]** > **[!UICONTROL Web Services]**.
1. Under **[!UICONTROL REST API]**, copy the **[!UICONTROL Endpoint]** URL. The format is `https://XXX-XXX-XXX.mktorest.com`.

## Configure your AI tool

Each AI tool reads MCP server configuration from a different location. Find your tool below and follow the steps to add the [!DNL Marketo] MCP server.

### Claude Desktop

The configuration file is `claude_desktop_config.json`. Open it from one of these locations:

- **macOS**: `~/Library/Application Support/Claude/claude_desktop_config.json`
- **Windows**: `%APPDATA%\Claude\claude_desktop_config.json`
- **Linux**: `~/.config/Claude/claude_desktop_config.json`

If the file already contains other MCP servers, add the `marketo` entry under `mcpServers`. The following example shows the complete `mcpServers` block:

```json
{
  "mcpServers": {
    "marketo": {
      "type": "http",
      "url": "https://marketo-mcp.adobe.io/mcp",
      "headers": {
        "X-Marketo-Client-Id": "YOUR-CLIENT-ID",
        "X-Marketo-Client-Secret": "YOUR-CLIENT-SECRET",
        "X-Marketo-Munchkin-Id": "YOUR-MUNCHKIN-ID"
      }
    }
  }
}
```

Save the file, quit Claude Desktop, and reopen it.

### Cursor

If your Cursor MCP configuration already contains other servers, add the `marketo` entry under `mcpServers`. The following example shows the complete `mcpServers` block in **[!UICONTROL Settings]** > **[!UICONTROL MCP]** or `.cursor/mcp.json` in your project directory:

```json
{
  "mcpServers": {
    "marketo": {
      "type": "http",
      "url": "https://marketo-mcp.adobe.io/mcp",
      "headers": {
        "X-Marketo-Client-Id": "YOUR-CLIENT-ID",
        "X-Marketo-Client-Secret": "YOUR-CLIENT-SECRET",
        "X-Marketo-Munchkin-Id": "YOUR-MUNCHKIN-ID"
      }
    }
  }
}
```

Restart Cursor.

### Claude Code (CLI)

Run the following command in your terminal, substituting your credentials:

```bash
claude mcp add --transport http marketo \
  https://marketo-mcp.adobe.io/mcp \
  --header "X-Marketo-Client-Id: YOUR-CLIENT-ID" \
  --header "X-Marketo-Client-Secret: YOUR-CLIENT-SECRET" \
  --header "X-Marketo-Munchkin-Id: YOUR-MUNCHKIN-ID"
```

### VS Code with GitHub Copilot

Open your VS Code `settings.json` by pressing **[!UICONTROL Ctrl+Shift+P]** or **[!UICONTROL Cmd+Shift+P]** on macOS, then selecting **[!UICONTROL Preferences: Open User Settings (JSON)]**. Add the following example:

```json
{
  "mcp": {
    "servers": {
      "marketo": {
        "type": "http",
        "url": "https://marketo-mcp.adobe.io/mcp",
        "headers": {
          "X-Marketo-Client-Id": "YOUR-CLIENT-ID",
          "X-Marketo-Client-Secret": "YOUR-CLIENT-SECRET",
          "X-Marketo-Munchkin-Id": "YOUR-MUNCHKIN-ID"
        }
      }
    }
  }
}
```

Press **[!UICONTROL Ctrl+Shift+P]** (or **[!UICONTROL Cmd+Shift+P]** on macOS), type **[!UICONTROL Reload Window]**, and press Enter.

>[!NOTE]
>
>For security purposes, use environment variable interpolation in configuration files instead of pasting credentials directly. You can reference variables using syntax like `${MARKETO_CLIENT_SECRET}` and set them in your environment. This prevents credentials from being stored in plain text in files that may be committed to version control.

## Available operations

Once connected, you can ask your AI assistant to perform operations across the following categories.

### Forms

Browse, create, clone, and approve forms. Add or remove fields, configure field visibility rules, and identify where forms are embedded.

Example prompts:

- "Show me all approved forms"
- "Clone the Contact Us form into the Q2 Campaign folder"
- "Add a Company field to the Demo Request form"

### Smart campaigns

Create smart campaigns, configure smart list filters, add flow steps, and activate or deactivate campaigns.

Example prompts:

- "What smart campaigns are active right now?"
- "Create a new smart campaign called Lead Scoring Update in the Operations folder"
- "Show me the flow steps in the Welcome Email campaign"

### Leads and lists

Find leads by email address, create or update lead records, and manage static list membership.

Example prompts:

- "Find the lead with email jane@example.com"
- "Add lead ID 12345 to the Q2 MQL list"
- "Create a new static list called Summer Event Attendees"

### Programs

Create, clone, and tag programs. Browse programs by type, channel, or date range.

Example prompts:

- "Clone the Q4 Webinar program into the 2026 Events folder"
- "Create a new email program called Summer Sale in the Campaigns folder"
- "Show me all programs tagged as Webinar"

### Emails and snippets

Browse emails, create emails from templates, update content sections, and manage reusable snippets.

Example prompts:

- "Show me all draft emails"
- "Update the header section of the Welcome Email"
- "What assets use the Holiday Promo snippet?"

### Instance structure

Browse folders, channels, tag types, and activity types to understand your [!DNL Marketo] configuration.

Example prompts:

- "List all folders in Marketo"
- "Show me all available channels"
- "What tag types are configured?"

### Bulk operations

Export lead data in bulk and check import or export job status.

Example prompts:

- "Create a bulk export of leads created in the last 30 days"
- "Check the status of export job xx"

## Troubleshooting

| Error | Cause | Fix |
| ------- | ------- | ----- |
| "Marketo endpoint not provided" | The `X-Marketo-Endpoint` header is missing from your configuration. | Re-check your MCP configuration and confirm all four headers are present. |
| "Marketo credentials not provided" | One or more of `X-Marketo-Client-Id`, `X-Marketo-Client-Secret`, or `X-Marketo-Munchkin-Id` is missing. | Verify all four headers are present in your configuration. |
| "Authentication Error" | Your credentials are invalid or expired. | Re-check your Client ID and Client Secret in **[!UICONTROL Admin]** > **[!UICONTROL LaunchPoint]**. |
| "403 Forbidden" | Your Munchkin ID is not on the server allowlist. | Contact your [!DNL Marketo] MCP administrator to add your Munchkin ID. |
| Connection timeout or refused | The MCP server is unreachable from your network. | Confirm you can reach the server URL from your environment. Check VPN requirements if applicable. |
| Tool calls return empty results | The API user lacks permissions for the requested asset type. | Ask your [!DNL Marketo] admin to review the API user role and permissions. |

## Frequently asked questions

### Is my data secure?

Credentials are transmitted in HTTP headers with each individual request. The server does not store or cache credentials between sessions, and each request is fully isolated.

### Can multiple people use this at the same time?

Yes. The server is multi-tenant. Each user connects with their own credentials, and requests are isolated from one another.

### What happens if my access token expires?

When you authenticate using Client ID and Client Secret, the server handles token refresh automatically. You do not need to take any action.

### Do I need to install or run anything?

No. The MCP server is hosted by Adobe. You only need to configure your AI tool to connect to it.

### What [!DNL Marketo] permissions does my API user need?

The API user needs access to the asset types you intend to manage. At minimum, assign a Read-Only role for browsing operations and a Read-Write role for creating or modifying assets. Work with your [!DNL Marketo] admin to assign appropriate permissions.

### What are the rate limits?

The MCP server inherits the API rate limits of the Marketo instance. Use a dedicated API user to track and manage quota consumption.

### Which AI tools are supported?

Claude Desktop, Cursor, Claude Code (CLI), and VS Code with GitHub Copilot. Any AI tool that supports the Model Context Protocol over HTTP should work.

### Can I connect to multiple [!DNL Marketo] instances?

Yes. Add multiple entries in your AI tool's MCP configuration, each with a unique name and the credentials for the corresponding instance. For example, you could configure `marketo-prod` and `marketo-staging` as separate servers.

## Security considerations

>[!IMPORTANT]
>
>Use a dedicated API user in [!DNL Marketo] with only the permissions required for your work. Do not reuse admin credentials for API access.

- **Per-request credentials.** Client ID, Client Secret, Munchkin ID, and the REST API endpoint are transmitted in HTTP headers with each request. The server does not store or cache them.
- **Multi-tenant isolation.** Each request uses its own set of credentials. Your data does not intersect with any other user's session.
- **Munchkin ID allowlist.** The server only accepts requests for approved [!DNL Marketo] instances. Requests using an unauthorized Munchkin ID are rejected with a 403 error.
- **Keep credentials out of version control.** Use environment variable interpolation (`${MARKETO_CLIENT_SECRET}`) if your AI tool supports it, so credentials are not stored in plain text in files committed to a repository.
