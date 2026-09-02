<div align="center">

# 🔭 Raygun MCP Server

### Investigate errors and performance in Raygun with AI assistants

[![MCP](https://img.shields.io/badge/MCP-Remote%20Server-blue?logo=anthropic&logoColor=white)](https://modelcontextprotocol.io/)
[![API](https://img.shields.io/badge/Raygun%20API-v3-FF6A13?logo=raygun&logoColor=white)](https://raygun.com/documentation/product-guides/raygun-api/)
[![Status](https://img.shields.io/badge/Status-Production-success?logo=checkmarx&logoColor=white)](https://api.raygun.com/v3/mcp)
[![Docs](https://img.shields.io/badge/Docs-Available-informational?logo=gitbook&logoColor=white)](https://github.com/MindscapeHQ/mcp-server-raygun/blob/main/TOOLS.md)

A remote Model Context Protocol (MCP) server that connects AI assistants to Raygun Crash Reporting, Real User Monitoring, and Application Performance Monitoring.

**[📚 Tool Reference](https://github.com/MindscapeHQ/mcp-server-raygun/blob/main/TOOLS.md)** • **[🚀 Quick Start](#getting-started)** • **[🔐 Authentication](#authentication)**

</div>

---

## ✨ Key Features

- 🐛 **Error Management** - Investigate, resolve, and track application errors and crashes with full stack traces and context
- 🚀 **Deployment Tracking** - Monitor releases and correlate errors with deployments to identify problematic changes
- ⚡ **Performance Insights** - Analyze page load times, user metrics, and performance trends over time
- 🔬 **APM Investigation** - Find backend hotspots, recurring performance issues, and slow traces
- 👥 **User Monitoring** - Track customer sessions, behavior patterns, and identify affected users
- 🤝 **Team Collaboration** - Manage invitations and coordinate error resolution across your team
- 📊 **Metrics & Analytics** - Time-series analysis and distribution histograms for errors and performance

## 📋 Requirements

- A [Raygun account](https://raygun.com/) with an active subscription
- An MCP client with OAuth support, or a [Raygun Personal Access Token](https://app.raygun.com/user/tokens)

## 🚀 Getting Started

The Raygun MCP server is hosted at:

```text
https://api.raygun.com/v3/mcp
```

### OAuth (recommended)

Add the URL as a Streamable HTTP server without an `Authorization` header. On first connection, your MCP client will open Raygun in your browser so you can sign in, select a plan, review the requested permissions, and authorize access.

You do not need to supply an OAuth client ID or client secret. Raygun supports automatic client registration.

<details>
<summary>Codex</summary>

```bash
codex mcp add raygun --url https://api.raygun.com/v3/mcp
codex mcp login raygun
```

In the ChatGPT desktop app, open **Settings > MCP servers**, select **Add server**, choose **Streamable HTTP**, and enter the Raygun endpoint. Save and restart the app, then select **Authenticate** for Raygun.

</details>

<details>
<summary>Claude Code</summary>

```bash
claude mcp add --transport http raygun https://api.raygun.com/v3/mcp
```

Run `/mcp` in Claude Code and follow the browser authentication flow.

</details>

<details>
<summary>Cursor</summary>

```json
{
  "mcpServers": {
    "raygun": {
      "url": "https://api.raygun.com/v3/mcp"
    }
  }
}
```

Cursor will prompt you to authenticate when it connects.

</details>

<details>
<summary>VS Code</summary>

```json
{
  "servers": {
    "raygun": {
      "type": "http",
      "url": "https://api.raygun.com/v3/mcp"
    }
  }
}
```

VS Code will prompt you to authenticate when it connects.

</details>

### Personal Access Token

PAT authentication remains supported for clients without MCP OAuth support and for automation. The following example uses Cursor's configuration format; other clients use the same `Authorization` header in their HTTP server configuration:

```json
{
  "mcpServers": {
    "raygun": {
      "url": "https://api.raygun.com/v3/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_PAT_TOKEN"
      }
    }
  }
}
```

### 💬 Your First Prompt

After configuration, try asking your AI assistant:

```
🔍 "Show me the most recent error groups in my Raygun applications"
```

```
🚀 "What were the latest deployments and did they introduce any new errors?"
```

```
📊 "Analyze the performance trends for my top pages over the last 7 days"
```

## 🛠️ Tools

The Raygun MCP server provides the following categories of tools:

<details>
<summary>📱 Applications</summary>

- `applications_list` - List all applications in your Raygun account
- `applications_search` - Search for applications by name
- `application_get_details` - Get detailed application information
- `application_regenerate_api_key` - Generate a new API key for an application

</details>

<details>
<summary>🐛 Error Management</summary>

- `error_groups_list` - List error groups within an application
- `error_groups_search` - Search occurrences by error, stack trace, URL, version, user, tags, or custom data
- `error_group_investigate` - Get complete details about a specific error group
- `error_group_update_status` - Change error group status (resolve, ignore, activate)
- `error_group_add_comment` - Add investigation notes to an error group
- `error_group_read_comments` - Review existing investigation notes
- `error_group_instances_list` - List occurrences in an error group
- `error_instance_get` - Get the full stack trace and context for an occurrence

</details>

<details>
<summary>🚀 Deployments</summary>

- `deployments_list` - List deployments for an application
- `deployment_create` - Create a new deployment record
- `deployment_get_latest` - Get the most recent deployment with error analysis
- `deployment_investigate` - Get comprehensive deployment information
- `deployment_manage` - Update or delete a deployment

</details>

<details>
<summary>👥 Customers & Sessions</summary>

- `customers_search` - Search customers by name, email, or identifier
- `customer_investigate` - Get customer profile, recent error groups, and sessions
- `sessions_list` - List user sessions with environment and device data
- `session_investigate` - Inspect a session's environment, errors, and page views

</details>

<details>
<summary>🔬 Application Performance Monitoring</summary>

- `apm_issues_search` - Find recurring backend performance issues and anti-patterns
- `apm_issue_investigate` - Inspect an issue's metrics and affected traces
- `apm_traces_search` - Find slow or failing backend requests
- `apm_trace_investigate` - Inspect profiler threads and significant calls in a trace
- `apm_hotspots_search` - Rank slow methods, database queries, and external calls

</details>

<details>
<summary>📊 Performance & Metrics</summary>

- `pages_list` - List monitored pages in an application
- `page_investigate` - Get page details for metrics queries
- `metrics_website_performance_analyze` - Track performance trends over time
- `metrics_performance_distribution_analyze` - Understand performance variability
- `metrics_error_trends_analyze` - Track error rates and patterns

</details>

<details>
<summary>🤝 Team Management</summary>

- `invitations_manage` - List and review team invitations
- `invitation_send` - Send a new team invitation
- `invitation_revoke` - Cancel a pending invitation

</details>

For detailed documentation on each tool, see the [Tool Reference](https://github.com/MindscapeHQ/mcp-server-raygun/blob/main/TOOLS.md).

## 🔐 Authentication

### OAuth

Raygun implements the MCP authorization flow for HTTP clients. The server advertises its authorization server through OAuth Protected Resource Metadata, and compatible clients register themselves automatically using Client ID Metadata Documents or Dynamic Client Registration.

Access is tied to the Raygun user, plan, and scopes approved on the consent screen. Compatible clients securely store and refresh their own tokens.

### Obtaining a Personal Access Token

PATs remain available when OAuth is not suitable:

1. Navigate to [**Raygun Personal Access Tokens**](https://app.raygun.com/user/tokens)
2. Click **Create New Token**
3. Give your token a descriptive name (e.g., "MCP Server Access")
4. Select the appropriate permissions for your use case
5. Copy the generated token and send it as `Authorization: Bearer YOUR_PAT_TOKEN`

Keep PATs secure and never commit them to version control.

For more details, see the [Raygun API documentation](https://raygun.com/documentation/product-guides/raygun-api/).

---

## 📖 About

The Raygun MCP server enables AI assistants to investigate Crash Reporting, RUM, and APM data; track deployments; analyze performance; and manage application monitoring through natural-language conversations.

## 🔗 Resources

- 📚 [Raygun Documentation](https://raygun.com/documentation/)
- 🔌 [Raygun API Reference](https://raygun.com/documentation/product-guides/raygun-api/)
- 🤖 [Model Context Protocol](https://modelcontextprotocol.io/)
- 🐛 [Report Issues](https://github.com/MindscapeHQ/mcp-server-raygun/issues)

---

<div align="center">

**Built with ❤️ by [Raygun](https://raygun.com)**

[![Raygun](https://img.shields.io/badge/Powered%20by-Raygun-FF6A13?style=for-the-badge&logo=data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjQiIGhlaWdodD0iMjQiIHZpZXdCb3g9IjAgMCAyNCAyNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPGNpcmNsZSBjeD0iMTIiIGN5PSIxMiIgcj0iMTIiIGZpbGw9IndoaXRlIi8+Cjwvc3ZnPgo=)](https://raygun.com)

</div>
