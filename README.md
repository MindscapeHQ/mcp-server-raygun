<div align="center">

# 🔭 Raygun MCP Server

### Connect your AI assistant to Raygun's Crash Reporting and Real User Monitoring

[![MCP](https://img.shields.io/badge/MCP-Remote%20Server-blue)](https://modelcontextprotocol.io/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

A remote Model Context Protocol (MCP) server that provides AI assistants with direct access to Raygun's application monitoring data through Raygun's API V3.

**[📚 Tool Reference](https://github.com/MindscapeHQ/mcp-server-raygun/blob/main/TOOLS.md)** • **[🚀 Quick Start](#getting-started)** • **[🔑 Get API Token](https://app.raygun.com/)**

</div>

---

## ✨ Key Features

<table>
<tr>
<td width="50%">

### 🐛 Error Management
Investigate, resolve, and track application errors and crashes with full stack traces and context

### 🚀 Deployment Tracking
Monitor releases and correlate errors with deployments to identify problematic changes

### ⚡ Performance Insights
Analyze page load times, user metrics, and performance trends over time

</td>
<td width="50%">

### 👥 User Monitoring
Track customer sessions, behavior patterns, and identify affected users

### 🤝 Team Collaboration
Manage invitations and coordinate error resolution across your team

### 📊 Metrics & Analytics
Time-series analysis and distribution histograms for errors and performance

</td>
</tr>
</table>

## 📋 Requirements

- 🔐 A [Raygun account](https://raygun.com/) with an active subscription
- 🔑 A [Raygun Personal Access Token (PAT)](https://raygun.com/documentation/product-guides/raygun-api/)

## 🚀 Getting Started

The Raygun MCP server is hosted remotely at `https://api.raygun.com/v3/mcp`. 

> **💡 Tip:** Choose your AI assistant below and follow the configuration instructions. Don't forget to replace `YOUR_PAT_TOKEN` with your actual Raygun Personal Access Token!

<details>
<summary>Amp</summary>

**Guide:** [Amp MCP Documentation](https://ampcode.com/manual)

On macOS: `~/Library/Application Support/Amp/amp_config.json`

```json
{
  "amp.mcpServers": {
    "Raygun": {
      "command": "npx",
      "args": [
        "mcp-remote",
        "https://api.raygun.com/v3/mcp",
        "--header",
        "Authorization: Bearer YOUR_PAT_TOKEN"
      ]
    }
  }
}
```

</details>

<details>
<summary>Claude Code</summary>

**Guide:** [Claude Code MCP Documentation](https://docs.anthropic.com/en/docs/claude-code/mcp)

```bash
claude mcp add raygun npx mcp-remote https://api.raygun.com/v3/mcp --header "Authorization: Bearer YOUR_PAT_TOKEN"
```

</details>

<details>
<summary>Cline</summary>

**Guide:** [Cline MCP Configuration](https://docs.cline.bot/mcp/configuring-mcp-servers)

On macOS: `~/Library/Application Support/Code/User/globalStorage/rooveterinaryinc.roo-cline/settings/cline_mcp_settings.json`  
On Windows: `%APPDATA%\Code\User\globalStorage\rooveterinaryinc.roo-cline\settings\cline_mcp_settings.json`

```json
{
  "mcpServers": {
    "Raygun": {
      "command": "npx",
      "args": [
        "mcp-remote",
        "https://api.raygun.com/v3/mcp",
        "--header",
        "Authorization: Bearer YOUR_PAT_TOKEN"
      ]
    }
  }
}
```

</details>

<details>
<summary>Codex</summary>

**Guide:** [Codex MCP Advanced Configuration](https://github.com/openai/codex/blob/main/docs/advanced.md#model-context-protocol-mcp)

**Command:**
```bash
codex mcp add raygun -- npx mcp-remote https://api.raygun.com/v3/mcp --header "Authorization: Bearer YOUR_PAT_TOKEN"
```

**Configuration for `.codex/config.toml` (Windows):**
```toml
[mcp_servers.raygun]
command = "cmd"
args = [
    "/c",
    "npx",
    "mcp-remote",
    "https://api.raygun.com/v3/mcp",
    "--header",
    "Authorization: Bearer YOUR_PAT_TOKEN"
]
env = { SystemRoot="C:\\Windows", PROGRAMFILES="C:\\Program Files" }
startup_timeout_ms = 20_000
```

</details>

<details>
<summary>Copilot CLI</summary>

1. Start Copilot CLI:
   ```bash
   copilot
   ```
2. Add a new MCP server:
   ```bash
   /mcp add
   ```
3. Configure the following fields and press `CTRL-S` to save:
   * **Server name:** `raygun`
   * **Server Type:** `[1] Local`
   * **Command:** `npx`
   * **Arguments:** `mcp-remote, https://api.raygun.com/v3/mcp, --header, Authorization: Bearer YOUR_PAT_TOKEN`

</details>

<details>
<summary>Copilot / VS Code</summary>

**Guide:** [VS Code MCP Servers](https://code.visualstudio.com/docs/copilot/customization/mcp-servers)

**Command:**
```bash
code --add-mcp '{"name":"Raygun","command":"npx","args":["mcp-remote","https://api.raygun.com/v3/mcp","--header","Authorization: Bearer YOUR_PAT_TOKEN"]}'
```

**Or manually configure:**
```json
{
  "name": "Raygun",
  "command": "npx",
  "args": [
    "mcp-remote",
    "https://api.raygun.com/v3/mcp",
    "--header",
    "Authorization: Bearer YOUR_PAT_TOKEN"
  ]
}
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

**Guide:** [Gemini CLI MCP Setup](https://github.com/google-gemini/gemini-cli/blob/main/docs/tools/mcp-server.md#how-to-set-up-your-mcp-server)

**Project-wide:**
```bash
gemini mcp add raygun npx mcp-remote https://api.raygun.com/v3/mcp --header "Authorization: Bearer YOUR_PAT_TOKEN"
```

**Globally:**
```bash
gemini mcp add -s user raygun npx mcp-remote https://api.raygun.com/v3/mcp --header "Authorization: Bearer YOUR_PAT_TOKEN"
```

**Or manually configure:**
```json
{
  "mcpServers": {
    "Raygun": {
      "command": "npx",
      "args": [
        "mcp-remote",
        "https://api.raygun.com/v3/mcp",
        "--header",
        "Authorization: Bearer YOUR_PAT_TOKEN"
      ]
    }
  }
}
```

</details>

<details>
<summary>Gemini Code Assist</summary>

**Guide:** [Gemini Code Assist MCP Configuration](https://cloud.google.com/gemini/docs/codeassist/use-agentic-chat-pair-programmer#configure-mcp-servers)

```json
{
  "mcpServers": {
    "Raygun": {
      "command": "npx",
      "args": [
        "mcp-remote",
        "https://api.raygun.com/v3/mcp",
        "--header",
        "Authorization: Bearer YOUR_PAT_TOKEN"
      ]
    }
  }
}
```

</details>

<details>
<summary>JetBrains AI Assistant & Junie</summary>

Go to `Settings | Tools | AI Assistant | Model Context Protocol (MCP)` → `Add`  
Or for Junie: `Settings | Tools | Junie | MCP Settings` → `Add`

```json
{
  "mcpServers": {
    "Raygun": {
      "command": "npx",
      "args": [
        "mcp-remote",
        "https://api.raygun.com/v3/mcp",
        "--header",
        "Authorization: Bearer YOUR_PAT_TOKEN"
      ]
    }
  }
}
```

</details>

<details>
<summary>Visual Studio</summary>

Go to your Visual Studio MCP config file (see the [Visual Studio docs](https://docs.microsoft.com/visualstudio/ide/ai-assisted-development))

```json
{
  "name": "Raygun",
  "command": "npx",
  "args": [
    "mcp-remote",
    "https://api.raygun.com/v3/mcp",
    "--header",
    "Authorization: Bearer YOUR_PAT_TOKEN"
  ]
}
```

</details>

<details>
<summary>Warp</summary>

Go to `Settings | AI | Manage MCP Servers` → `+ Add`

```json
{
  "mcpServers": {
    "Raygun": {
      "command": "npx",
      "args": [
        "mcp-remote",
        "https://api.raygun.com/v3/mcp",
        "--header",
        "Authorization: Bearer YOUR_PAT_TOKEN"
      ]
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

- `customers_list` - List customers for an application
- `customer_investigate` - Get detailed customer information
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

1. 🔐 Log in to your [Raygun account](https://app.raygun.com/)
2. ⚙️ Navigate to **User Settings** > **Personal Access Tokens**
3. ➕ Click **Create New Token**
4. 📝 Give your token a descriptive name (e.g., "MCP Server Access")
5. ✅ Select the appropriate permissions for your use case
6. 📋 Copy the generated token and use it in your MCP configuration

> **⚠️ Important:** Replace `YOUR_PAT_TOKEN` in the configuration examples above with your actual token. Keep your token secure and never commit it to version control!

For more details, see the [Raygun API documentation](https://raygun.com/documentation/product-guides/raygun-api/).

---

## 📖 About

The Raygun MCP server enables AI coding assistants to interact with your Raygun Crash Reporting and Real User Monitoring applications, helping you investigate errors, track deployments, analyze performance, and manage your application monitoring workflow—all through natural language conversations.

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
