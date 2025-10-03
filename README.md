# Raygun MCP Server

A remote Model Context Protocol (MCP) server that provides AI assistants with direct access to Raygun's Crash Reporting and Real User Monitoring data through Raygun's API V3.

**[Tool Reference](https://github.com/MindscapeHQ/mcp-server-raygun/blob/main/TOOLS.md)**

## Key Features

- **Error Management** - Investigate, resolve, and track application errors and crashes
- **Deployment Tracking** - Monitor releases and correlate errors with deployments  
- **Performance Insights** - Analyze page load times, user metrics, and performance trends
- **User Monitoring** - Track customer sessions, behavior patterns, and affected users
- **Team Collaboration** - Manage invitations and coordinate error resolution

## Requirements

- A [Raygun account](https://raygun.com/) with an active subscription
- A [Raygun Personal Access Token (PAT)](https://raygun.com/documentation/product-guides/raygun-api/)

## Getting Started

The Raygun MCP server is hosted remotely at `https://api.raygun.com/v3/mcp`. Configure your AI coding assistant to connect using your Raygun Personal Access Token.

### Amp

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

### Cursor

Add to your Cursor MCP settings:

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

### Claude Desktop

On macOS: `~/Library/Application Support/Claude/claude_desktop_config.json`  
On Windows: `%APPDATA%\Claude\claude_desktop_config.json`

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

### Cline

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

### Your First Prompt

After configuration, try asking your AI assistant:

> "Show me the most recent error groups in my Raygun applications"

or

> "What were the latest deployments and did they introduce any new errors?"

## Tools

The Raygun MCP server provides the following categories of tools:

### Applications
- `applications_list` - List all applications in your Raygun account
- `applications_search` - Search for applications by name
- `application_get_details` - Get detailed application information
- `application_regenerate_api_key` - Generate a new API key for an application

### Error Management
- `error_groups_list` - List error groups within an application
- `error_group_investigate` - Get complete details about a specific error group
- `error_group_update_status` - Change error group status (resolve, ignore, activate)
- `error_group_add_comment` - Add investigation notes to an error group
- `error_instances_browse` - Browse individual error occurrences
- `error_instance_get_details` - Get full stack trace and context for an error instance

### Deployments
- `deployments_list` - List deployments for an application
- `deployment_create` - Create a new deployment record
- `deployment_get_latest` - Get the most recent deployment with error analysis
- `deployment_investigate` - Get comprehensive deployment information
- `deployment_manage` - Update or delete a deployment

### Customers & Sessions
- `customers_list` - List customers for an application
- `customer_investigate` - Get detailed customer information
- `sessions_list` - List user sessions with environment and device data

### Performance & Metrics
- `pages_list` - List monitored pages in an application
- `page_investigate` - Get page details for metrics queries
- `metrics_website_performance_analyze` - Track performance trends over time
- `metrics_performance_distribution_analyze` - Understand performance variability
- `metrics_error_trends_analyze` - Track error rates and patterns

### Team Management
- `invitations_manage` - List and review team invitations
- `invitation_send` - Send a new team invitation
- `invitation_revoke` - Cancel a pending invitation

For detailed documentation on each tool, see the [Tool Reference](https://github.com/MindscapeHQ/mcp-server-raygun/blob/main/TOOLS.md).

## Configuration

### Obtaining a Personal Access Token

To use the Raygun MCP server, you need a Raygun Personal Access Token (PAT):

1. Log in to your [Raygun account](https://app.raygun.com/)
2. Navigate to **User Settings** > **Personal Access Tokens**
3. Click **Create New Token**
4. Give your token a descriptive name (e.g., "MCP Server Access")
5. Select the appropriate permissions for your use case
6. Copy the generated token and use it in your MCP configuration

Replace `YOUR_PAT_TOKEN` in the configuration examples above with your actual token.

For more details, see the [Raygun API documentation](https://raygun.com/documentation/product-guides/raygun-api/).

## About

The Raygun MCP server enables AI coding assistants to interact with your Raygun Crash Reporting and Real User Monitoring applications, helping you investigate errors, track deployments, analyze performance, and manage your application monitoring workflow.

## Resources

- [Raygun Documentation](https://raygun.com/documentation/)
- [Raygun API Reference](https://raygun.com/documentation/product-guides/raygun-api/)
- [Model Context Protocol](https://modelcontextprotocol.io/)
- [Report Issues](https://github.com/MindscapeHQ/mcp-server-raygun/issues)
