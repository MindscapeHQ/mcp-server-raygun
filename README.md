<div align="center">

# 🔭 Raygun MCP Server

### Access your crash reporting data in Raygun with AI assistants

[![MCP](https://img.shields.io/badge/MCP-Remote%20Server-blue?logo=anthropic&logoColor=white)](https://modelcontextprotocol.io/)
[![API](https://img.shields.io/badge/Raygun%20API-v3-FF6A13?logo=raygun&logoColor=white)](https://raygun.com/documentation/product-guides/raygun-api/)
[![Status](https://img.shields.io/badge/Status-Production-success?logo=checkmarx&logoColor=white)](https://api.raygun.com/v3/mcp)
[![Docs](https://img.shields.io/badge/Docs-Available-informational?logo=gitbook&logoColor=white)](https://github.com/MindscapeHQ/mcp-server-raygun/blob/main/TOOLS.md)

A remote Model Context Protocol (MCP) server that connects AI assistants to your crash reporting and real user monitoring data in Raygun through natural language conversations.

**[📚 Tool Reference](https://github.com/MindscapeHQ/mcp-server-raygun/blob/main/TOOLS.md)** • **[🚀 Quick Start](#getting-started)** • **[🔑 Get API Token](https://app.raygun.com/user/tokens)**

</div>

---

## ✨ Key Features

- 🐛 **Error Management** - Investigate, resolve, and track application errors and crashes with full stack traces and context
- 🚀 **Deployment Tracking** - Monitor releases and correlate errors with deployments to identify problematic changes
- ⚡ **Performance Insights** - Analyze page load times, user metrics, and performance trends over time
- 👥 **User Monitoring** - Track customer sessions, behavior patterns, and identify affected users
- 🤝 **Team Collaboration** - Manage invitations and coordinate error resolution across your team
- 📊 **Metrics & Analytics** - Time-series analysis and distribution histograms for errors and performance

## 📋 Requirements

- 🔐 A [Raygun account](https://raygun.com/) with an active subscription
- 🔑 A [Raygun Personal Access Token (PAT)](https://app.raygun.com/user/tokens)

## 🚀 Getting Started

The Raygun MCP server is hosted remotely at `https://api.raygun.com/v3/mcp`. 

> **💡 Tip:** Choose your AI assistant below and follow the configuration instructions. Don't forget to replace `YOUR_PAT_TOKEN` with your actual Raygun Personal Access Token!

<details>
<summary>Amp</summary>

**Guide:** [Amp MCP Documentation](https://ampcode.com/manual#mcp)

```bash
amp mcp add raygun --header "Authorization=Bearer YOUR_PAT_TOKEN" https://api.raygun.com/v3/mcp
```

</details>

<details>
<summary>Claude Code</summary>

**Guide:** [Claude Code MCP Documentation](https://docs.claude.com/en/docs/claude-code/mcp)

```bash
claude mcp add --transport http raygun https://api.raygun.com/v3/mcp --header "Authorization: Bearer YOUR_PAT_TOKEN"
```

</details>

<details>
<summary>Cline</summary>

**Guide:** [Cline MCP Documentation](https://docs.cline.bot/mcp/connecting-to-a-remote-server)

Use `https://api.raygun.com/v3/mcp` and your PAT token

</details>

<details>
<summary>Codex</summary>

**Guide:** [Codex MCP Documentation](https://developers.openai.com/codex/mcp/)

```toml
[mcp_servers.raygun]
command = "npx"
args = ["mcp-remote", "https://api.raygun.com/v3/mcp", "--header", "Authorization: Bearer YOUR_PAT_TOKEN"]
```

</details>

<details>
<summary>Cursor</summary>

Go to `Cursor Settings` → `MCP` → `New MCP Server`

```json
{
  "mcpServers": {
    "Raygun": {
      "url": "https://api.raygun.com/v3/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_PAT_TOKEN"
      }
    }
  }
}
```

</details>

<details>
<summary>Gemini CLI</summary>

```bash
gemini mcp add --transport http raygun https://api.raygun.com/v3/mcp --header "Authorization: Bearer YOUR_PAT_TOKEN"
```

</details>

<details>
<summary>JetBrains AI Assistant</summary>

**Guide:** [JetBrains AI Assistant MCP Documentation](https://www.jetbrains.com/help/ai-assistant/mcp.html#connect-to-an-mcp-server)

```json
{
  "mcpServers": {
    "Raygun": {
      "url": "https://api.raygun.com/v3/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_PAT_TOKEN"
      }
    }
  }
}
```

</details>

<details>
<summary>VS Code</summary>

**Guide:** [VS Code MCP Servers](https://code.visualstudio.com/docs/copilot/customization/mcp-servers)

```json
{
  "servers": {
    "raygun": {
      "url": "https://api.raygun.com/v3/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_PAT_TOKEN"
      }
    }
  }
}
```

</details>

<details>
<summary>Zed</summary>

**Guide:** [Zed MCP Documentation](https://zed.dev/docs/ai/mcp)

```json
{
  "context_servers": {
    "raygun": {
      "source": "custom",
      "command": "npx",
      "args": [
        "mcp-remote",
        "https://api.raygun.com/v3/mcp",
        "--header",
        "Authorization: Bearer YOUR_PAT_TOKEN"
      ],
      "env": {}
    }
  }
}
```

</details>

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
- `error_group_investigate` - Get complete details about a specific error group
- `error_group_update_status` - Change error group status (resolve, ignore, activate)
- `error_group_add_comment` - Add investigation notes to an error group
- `error_instances_browse` - Browse individual error occurrences
- `error_instance_get_details` - Get full stack trace and context for an error instance

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

## 🔑 Configuration

### Obtaining a Personal Access Token

To use the Raygun MCP server, you need a Raygun Personal Access Token (PAT):

1. Navigate to [**Raygun Personal Access Tokens**](https://app.raygun.com/user/tokens)
2. Click **Create New Token**
3. Give your token a descriptive name (e.g., "MCP Server Access")
4. Select the appropriate permissions for your use case
5. Copy the generated token and use it in your MCP configuration

> **⚠️ Important:** Replace `YOUR_PAT_TOKEN` in the configuration examples above with your actual token. Keep your token secure and never commit it to version control!

For more details, see the [Raygun API documentation](https://raygun.com/documentation/product-guides/raygun-api/).

---

## 📖 About

The Raygun MCP server enables AI coding assistants to access and analyze your crash reporting and real user monitoring data in Raygun, helping you investigate errors, track deployments, analyze performance, and manage your application monitoring workflow—all through natural language conversations.

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

## Hosted deployment

A hosted deployment is available on [Fronteir AI](https://fronteir.ai/mcp/mindscapehq-server-raygun).

