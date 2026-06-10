---
title: Marketo Engage MCP Server
description: Learn how to connect an AI assistant to Marketo using the Marketo Engage MCP server. Configure Claude Desktop, Cursor, Claude Code, or VS Code with your Marketo credentials.
badgeBeta: label="Limited Availability" type="informative" tooltip="This feature is currently in a limited beta release"
exl-id: ab446e56-6250-4af5-b03e-162991d09a5c
autotag-review: '2026-06-02T13:31:15.329Z'
TQID: 'https://experienceleague.adobe.com/PJJm7yv8HmbwMB2fsnfDCXs8zprDJK5Q5z2uiiCJRZI'
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
    internal-label: Marketo Engage
feature_v2:
  - id: a7170d27-32ab-462b-a333-269abc654483
    internal-label: Smart Campaigns
  - id: b0bb9048-d951-48d8-8232-45cf248a7e27
    internal-label: Forms
  - id: b13bd2ad-8e65-49e5-9691-2a0d31067b35
    internal-label: Integrations
  - id: b3b8a63f-51fc-40f6-a7d2-a31c5d49fb45
    internal-label: Configuration
  - id: c2dbad80-0f5c-4d96-a798-2a65f93b8721
    internal-label: Assets
  - id: dca84292-69e9-4116-a575-667d31fa060d
    internal-label: APIs
  - id: e2290edd-b061-4880-9d79-dee306cf5aa9
    internal-label: Implementation
  - id: e64968b2-4ee5-47f9-8cae-0588f184b9eb
    internal-label: Programs
  - id: f82558ea-6af5-44eb-a424-5b3389abb0a3
    internal-label: Templates
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: bbbea26f-9621-49eb-9ab8-e06fb3bbce8c
    internal-label: Artificial intelligence
---
# [!DNL Marketo Engage] MCP Server

>[!AVAILABILITY] 
>
> This feature is in limited availability. To request access, fill out [this form](https://forms.cloud.microsoft/Pages/ResponsePage.aspx?id=Wht7-jR7h0OUrtLBeN7O4Y-uSf63sAxCmWyqMJg8eMFUMVZSVExSNDA3T0I4SEcwRDFSVTBGWU01Uy4u&origin=QRCode){target="_blank"}. Be sure to have your subscription's Munchkin ID ready.

Model Context Protocol (MCP) is an open standard that enables AI tools to communicate with external services. The [!DNL Marketo] MCP server acts as a bridge between your AI assistant and [!DNL Marketo]. It exposes more than 100 operations across forms, programs, smart campaigns, leads, emails, snippets, lists, and folders.

When your AI tool calls the MCP server, the server executes the corresponding REST API call on your behalf, using the credentials you provide in each request. You do not need to install, deploy, or run any server-side software.


>[!IMPORTANT]
>
>The Model Context Protocol (MCP) is an emerging open-source standard and may present security or reliability risks. Adobe MCP server integrations and related documentation are provided "as is," without warranties of any kind.
>Connecting MCP clients or servers to Adobe products is a customer-elected configuration, and customers are responsible for evaluating the security and suitability of any MCP integration. Adobe is not responsible for issues arising from misconfiguration, misuse of the MCP, vulnerabilities in third-party implementations, or unintended actions performed through MCP-enabled workflows.
>To reduce risk, Adobe encourages testing integrations in a sandbox environment prior to productive use and carefully reviewing and validating all MCP-initiated actions and responses before confirming or relying on them.

## MCP basics

>Think of MCP like a USB-C port for AI applications. Just as USB-C provides a standardized way to connect your devices to various peripherals and accessories, MCP provides a standardized way to connect AI models to data sources and tools. — [Model Context Protocol](https://modelcontextprotocol.io/docs/getting-started/intro){target="_blank"}

MCP allows an AI tool to connect to multiple external services at the same time. For example, an AI assistant could:

* Connect to a word processor for AI-assisted document generation
* Connect to animation tools, such as Blender, for build visualizations
* Connect to Adobe After Effects for video editing

MCP is a communication protocol: an open standard that any application can implement to expose its data and actions to AI tools.

## What [!DNL Marketo Engage] MCP does and does not do

Understanding the scope of MCP helps set expectations before you connect your AI tool.

**MCP does:**

* Provide access to [!DNL Marketo] data and capabilities through standard REST APIs
* Execute API calls on your behalf using credentials you supply with each request
* Support multiple simultaneous users, each connected with their own credentials
* Handle OAuth token refresh automatically. You do not need to manage token expiration
* Operate within tenant-isolated environments so your data never intersects with another user's session

**MCP does not:**

* Use, host, or run any AI or machine learning models. All AI processing happens in your AI tool, not in the MCP
* Train on or learn from any data, including your customer data
* Generate predictions, recommendations, or decisions. Decision-making is the responsibility of the downstream AI tool or user
* Store or retain credentials, request data, or session state between requests
* Require you to install, deploy, or manage any server-side software

MCP may transmit data, including potentially sensitive fields, depending on API usage but B2B data involves customer business data and does not involve PII data.

## Prerequisites

* A [!DNL Marketo] instance with REST API access enabled
* Admin access to create API credentials in [!DNL Marketo] LaunchPoint
* One of the following AI tools: Claude Desktop, Cursor, Codex, Claude Code (CLI), or VS Code with GitHub Copilot
* Network access to the MCP server URL: `https://marketo-mcp.adobe.io/mcp`

## Get Marketo credentials

You need the following values from your [!DNL Marketo] instance:

* **Client ID**
* **Client Secret**
* **Munchkin Account ID**

If you already have them, skip to [Configure your AI tool](#configure-your-ai-tool).

### Client ID and Client Secret

1. Go to **[!UICONTROL Admin]** > **[!UICONTROL LaunchPoint]**.
1. Select your API service. If you do not have one, select **[!UICONTROL New]** > **[!UICONTROL New Service]**, choose **[!UICONTROL Custom]** as the service type, and assign a dedicated API user.
1. Select **[!UICONTROL View Details]** and copy the **[!UICONTROL Client ID]** and **[!UICONTROL Client Secret]** values.

### Munchkin Account ID

1. Go to **[!UICONTROL Admin]** > **[!UICONTROL Munchkin]**.
1. Copy the **[!UICONTROL Munchkin Account ID]**. The format is `XXX-XXX-XXX` and matches the prefix of your instance URL.

## Configure your AI tool

Each AI tool has a slightly different setup. Connection examples are provided for common tools.

* [Claude Desktop](#claude-desktop)
* [Cursor](#cursor)
* [Claude Code CLI](#claude-code)
* [OpenAI Codex](#codex)
* [VSCode with GitHub Copilot](#vscode)

>[!TIP]
>
>To connect to multiple [!DNL Marketo] instances, add separate entries in your MCP configuration with unique names: `marketo-prod` and `marketo-staging`, each with the corresponding credentials.

### Claude Desktop {#claude-desktop}

To connect to Claude Desktop, download [marketo-mcp-bridge.zip](assets/marketo-mcp-bridge.zip) and unpack it. Put `marketo-mcp-bridge.mjs` into a known location so you can refer in the next step.

You will also need:

* Node.js v18+
* npm

1. Open Claude Desktop
1. Go to **Settings > Developer > Edit Config**
1. Add the following to `claude_desktop_config.json`:

```json
{
  "preferences": {
    ...
  },
  "mcpServers": {
    "marketo-mcp": {
      "command": "node",
      "args": ["/path/to/marketo-bridge/bridge.mjs"],
      "env": {
        "MARKETO_MCP_PROD_CLIENT_ID": "<your-client-id>",
        "MARKETO_MCP_PROD_CLIENT_SECRET": "<your-client-secret>",
        "MARKETO_MCP_PROD_MUNCHKIN_ID": "<your-munchkin-id>"
      }
    }
  }
}
```

1. Restart Claude Desktop

### Cursor {#cursor}

If your Cursor MCP configuration already contains other servers, add the `marketo` entry under `mcpServers`. The following example shows the complete `mcpServers` block in **[!UICONTROL Settings]** > **[!UICONTROL MCP]** or `.cursor/mcp.json` in your project directory:

>[!BEGINTABS]

>[!TAB Marketo client credentials]

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

>[!TAB IMS token]

```json
{
  "mcpServers": {
    "marketo": {
      "type": "http",
      "url": "https://marketo-mcp.adobe.io/mcp",
      "headers": {
        "Authorization": "Bearer YOUR-IMS-TOKEN",
        "x-gw-ims-org-id": "YOUR-IMS-ORG-ID"
      }
    }
  }
}
```

>[!ENDTABS]

Restart Cursor.

### Claude Code (CLI) {#claude-code}

Run the following command in your terminal, substituting your credentials:

>[!BEGINTABS]

>[!TAB Marketo client credentials]

```bash
claude mcp add --transport http marketo \
  https://marketo-mcp.adobe.io/mcp \
  --header "X-Marketo-Client-Id: YOUR-CLIENT-ID" \
  --header "X-Marketo-Client-Secret: YOUR-CLIENT-SECRET" \
  --header "X-Marketo-Munchkin-Id: YOUR-MUNCHKIN-ID"
```

>[!TAB IMS token]

```bash
claude mcp add --transport http marketo \
  https://marketo-mcp.adobe.io/mcp \
  --header "Authorization: Bearer YOUR-IMS-TOKEN" \
  --header "x-gw-ims-org-id: YOUR-IMS-ORG-ID"
```

>[!ENDTABS]

### OpenAI Codex {#codex}

1. Go to Settings > MCP Servers > Add Server
1. Add the server URL: `https://marketo-mcp.adobe.io/mcp`
1. Add the headers for your authentication method:

>[!BEGINTABS]

>[!TAB Marketo client credentials]

* X-Marketo-Client-Id: "YOUR-CLIENT-ID"
* X-Marketo-Client-Secret: "YOUR-CLIENT-SECRET"
* X-Marketo-Munchkin-Id: "YOUR-MUNCHKIN-ID"

>[!TAB IMS token]

* Authorization: "Bearer YOUR-IMS-TOKEN"
* x-gw-ims-org-id: "YOUR-IMS-ORG-ID"

>[!ENDTABS]

1. Click Save to complete the process.


### VS Code with GitHub Copilot {#vscode}

Press **[!UICONTROL Ctrl+Shift+P]** (or **[!UICONTROL Cmd+Shift+P]** on macOS), type **[!UICONTROL MCP: Open User Configuration]**, and press Enter. This opens `mcp.json`. Add the `marketo` entry inside the `servers` object:

>[!BEGINTABS]

>[!TAB Marketo client credentials]

```json
{
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
```

>[!TAB IMS token]

```json
{
  "servers": {
    "marketo": {
      "type": "http",
      "url": "https://marketo-mcp.adobe.io/mcp",
      "headers": {
        "Authorization": "Bearer YOUR-IMS-TOKEN",
        "x-gw-ims-org-id": "YOUR-IMS-ORG-ID"
      }
    }
  }
}
```

>[!ENDTABS]

>[!NOTE]
>
>For security purposes, use environment variable interpolation in configuration files instead of pasting credentials directly. You can reference variables using syntax like `${MARKETO_CLIENT_SECRET}` and set them in your environment. This prevents credentials from being stored in plain text in version-controlled files.

## Available operations

Once connected, you can ask your AI assistant to perform operations across the following categories. For the complete list of supported operations with API references, see [Supported MCP operations](mcp-server-operations.md).

### Forms

Browse, create, clone, and approve forms. Add or remove fields, configure field visibility rules, and identify where forms are embedded.

Example prompts:

* "Show me all approved forms"
* "Clone the Contact Us form into the Q2 Campaign folder"
* "Add a Company field to the Demo Request form"

### Smart campaigns

Create smart campaigns, configure smart list filters, add flow steps, and activate or deactivate campaigns.

Example prompts:

* "What smart campaigns are active right now?"
* "Create a new smart campaign called Lead Scoring Update in the Operations folder"
* "Show me the flow steps in the Welcome Email campaign"

### Leads and lists

Find leads by email address, create or update lead records, and manage static list membership.

Example prompts:

* "Find the lead with email jane@example.com"
* "Add lead ID 12345 to the Q2 MQL list"
* "Create a new static list called Summer Event Attendees"

### Programs

Create, clone, and tag programs. Browse programs by type, channel, or date range.

Example prompts:

* "Clone the Q4 Webinar program into the 2026 Events folder"
* "Create a new email program called Summer Sale in the Campaigns folder"
* "Show me all programs tagged as Webinar"

### Emails and snippets

Browse emails, create emails from templates, update content sections, and manage reusable snippets.

Example prompts:

* "Show me all draft emails"
* "Update the header section of the Welcome Email"
* "What assets use the Holiday Promo snippet?"

### Instance structure

To understand your [!DNL Marketo] configuration, browse folders, channels, tag types, and activity types.

Example prompts:

* "List all folders in Marketo"
* "Show me all available channels"
* "What tag types are configured?"

### Bulk operations

Export lead data in bulk and check import or export job status.

Example prompts:

* "Create a bulk export of leads created in the last 30 days"
* "Check the status of export job xx"

## Troubleshooting

| Error | Cause | Fix |
| ------- | ------- | ----- |
| "Marketo credentials not provided" | One or more of `X-Marketo-Client-Id`, `X-Marketo-Client-Secret`, or `X-Marketo-Munchkin-Id` is missing. | Verify all Marketo client credential headers are present in your configuration. |
| "401 Unauthorized" | Your credentials are missing, invalid, or expired. With Marketo client credentials, the Client ID or Client Secret is incorrect. With an IMS token, the token is invalid or expired. | Verify the credentials for your authentication method. For client credentials, re-check the **[!UICONTROL Client ID]** and **[!UICONTROL Client Secret]** in **[!UICONTROL Admin]** > **[!UICONTROL LaunchPoint]**. For an IMS token, generate a new token and update the `Authorization` header. |
| "403 Forbidden" | Your credentials are valid, but your [!DNL Marketo] instance is not enabled for MCP access. | Contact your [!DNL Marketo] MCP administrator to enable MCP access for your Munchkin Account ID. |
| "Too many requests" (rate limit) | You sent too many requests in a short period, or too many requests at the same time, and reached your [!DNL Marketo] instance's API limits. | Reduce how frequently and how many requests you send at once, and wait a short time before retrying. Use a dedicated API user to track and manage your quota. |
| Connection timeout or refused | The MCP server is unreachable from your network. | Confirm you can reach the server URL from your environment. Check VPN requirements if applicable. |
| Tool calls return empty results | The API user lacks permissions for the requested asset type. | Ask your [!DNL Marketo] admin to review the API user role and permissions. |

## Security considerations

>[!IMPORTANT]
>
>Use a dedicated API user in [!DNL Marketo] with only the permissions required for your work. Do not reuse admin credentials for API access.

* **Per-request credentials.** Client ID, Client Secret, Munchkin ID, and the REST API endpoint are transmitted in HTTP headers with each request. The server does not store or cache them.
* **Multi-tenant isolation.** Each request uses its own set of credentials. Your data does not intersect with any other user's session.
* **Munchkin ID allowlist.** The server only accepts requests for approved [!DNL Marketo] instances. Requests using an unauthorized Munchkin ID are rejected with a 403 error.
* **API rate limits.** The MCP server inherits the API rate limits of your [!DNL Marketo] instance. Use a dedicated API user to track and manage quota consumption.
* **Keep credentials out of version control.** Use environment variable interpolation (`${MARKETO_CLIENT_SECRET}`) if your AI tool supports it, so credentials are not stored in plain text in repository files.
