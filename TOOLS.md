# Raygun MCP Tools Reference

This document provides detailed documentation for all tools available in the Raygun MCP server.

## Table of Contents

- [Applications](#applications)
- [Error Management](#error-management)
- [Deployments](#deployments)
- [Customers & Sessions](#customers--sessions)
- [Performance & Metrics](#performance--metrics)
- [Team Management](#team-management)

---

## Applications

### `applications_list`

List applications available to the current user.

**Parameters:**
- `count` (integer, optional): Maximum number of applications to return (default: 100, max: 500)
- `offset` (integer, optional): Number of applications to skip for pagination (0-based)
- `sortOrder` (string, optional): Sort order for results. Available fields: `identifier`, `name`, `planIdentifier`. Add `asc` or `desc`. Examples: `name asc`, `identifier desc`

**Example:**
```
List my Raygun applications sorted by name
```

---

### `applications_search`

Search for applications by name.

**Parameters:**
- `searchTerm` (string, required): Search term to match against application names (case-insensitive partial matching)
- `limit` (integer, optional): Maximum number of matching applications to return (default: 50, max: 200)

**Example:**
```
Search for applications named "production"
```

---

### `application_get_details`

Get detailed information about a specific application including settings, API keys, plan information, and status.

**Parameters:**
- `appId` (string, required): The unique identifier of the application

**Example:**
```
Get details for application abc123
```

---

### `application_regenerate_api_key`

Generate a new API key for an application. **Warning:** This will invalidate the existing API key immediately.

**Parameters:**
- `appId` (string, required): The unique identifier of the application

**Example:**
```
Regenerate the API key for application abc123
```

---

## Error Management

### `error_groups_list`

List error groups within a Raygun application to understand what errors are occurring.

**Parameters:**
- `appId` (string, required): The unique identifier of the Raygun application
- `count` (integer, optional): Maximum number of error groups to return (default: 100, max: 500)
- `offset` (integer, optional): Number of error groups to skip for pagination (0-based)
- `sortOrder` (string, optional): Sort order for results. Available fields: `identifier`, `message`, `status`, `lastOccurredAt`, `createdAt`. Examples: `lastOccurredAt desc` (newest first), `message asc` (alphabetical)

**Example:**
```
List the most recent error groups for application abc123
```

---

### `error_group_investigate`

Get complete details about a specific error group including its first occurrence with stack trace, tags, and context.

**Parameters:**
- `appId` (string, required): The unique identifier of the Raygun application
- `errorGroupId` (string, required): The unique identifier of the error group

**Example:**
```
Investigate error group xyz789 in application abc123
```

---

### `error_group_update_status`

Change the status of an error group (activate, resolve, ignore, permanently ignore).

**Parameters:**
- `appId` (string, required): The unique identifier of the Raygun application
- `errorGroupId` (string, required): The unique identifier of the error group
- `status` (string, required): New status. Options: `active`, `resolved`, `ignored`, `permanently_ignored`
- `resolvedVersion` (string, optional): For `resolved` status - version where error was fixed
- `discardFromPreviousVersions` (boolean, optional): For `resolved` status - whether to discard occurrences from previous versions (default: false)
- `discardNewOccurrences` (boolean, optional): For `permanently_ignored` status - whether to automatically discard new occurrences (default: false)

**Example:**
```
Resolve error group xyz789 in application abc123 as fixed in version 2.1.0
```

---

### `error_group_add_comment`

Add a comment to an error group to document investigation findings or resolution steps.

**Parameters:**
- `appId` (string, required): The unique identifier of the Raygun application
- `errorGroupId` (string, required): The unique identifier of the error group
- `comment` (string, required): The comment text to add

**Example:**
```
Add a comment to error group xyz789: "Fixed by updating the authentication module"
```

---

### `error_instances_browse`

Browse individual error instances within an error group to see patterns across occurrences.

**Parameters:**
- `appId` (string, required): The unique identifier of the Raygun application
- `errorGroupId` (string, required): The unique identifier of the error group
- `count` (integer, optional): Maximum number of error instances to return (default: 100, max: 500)
- `offset` (integer, optional): Number of error instances to skip for pagination (0-based)
- `sortOrder` (string, optional): Sort order. Available fields: `occurredOn`, `identifier`. Examples: `occurredOn desc` (newest first)

**Example:**
```
Show me the latest error instances for error group xyz789
```

---

### `error_instance_get_details`

Get detailed information about a specific error instance including full stack trace and environment data.

**Parameters:**
- `appId` (string, required): The unique identifier of the Raygun application
- `errorGroupId` (string, required): The unique identifier of the error group
- `errorInstanceId` (string, required): The unique identifier of the error instance (accepts Base36 and numeric formats)

**Example:**
```
Get full details for error instance 12345 in error group xyz789
```

---

## Deployments

### `deployments_list`

List deployments for a Raygun application to track releases and software versions.

**Parameters:**
- `appId` (string, required): The unique identifier of the Raygun application
- `count` (integer, optional): Maximum number of deployments to return (default: 100, max: 500)
- `offset` (integer, optional): Number of deployments to skip for pagination (0-based)
- `sortOrder` (string, optional): Sort order. Available fields: `identifier`, `version`, `deployedAt`, `createdAt`. Examples: `deployedAt desc` (newest first)

**Example:**
```
List recent deployments for application abc123
```

---

### `deployment_create`

Create a new deployment record to track a software release.

**Parameters:**
- `appId` (string, optional): The unique identifier of the Raygun application (optional if using apiKey)
- `apiKey` (string, optional): The Raygun API key for the application (optional if using appId)
- `payload` (object, required): Deployment information including:
  - `Version` (string, required): Version identifier
  - `DeployedAt` (datetime, optional): Deployment timestamp
  - `CreatedAt` (datetime, optional): Creation timestamp
  - `OwnerName` (string, optional): Name of person who deployed
  - `EmailAddress` (string, optional): Email of person who deployed
  - `Comment` (string, optional): Deployment notes
  - `ScmType` (string, optional): Source control type (`gitHub`, `bitbucket`, `gitLab`, `azureDevOps`)
  - `ScmIdentifier` (string, optional): Commit SHA or identifier

**Example:**
```
Create a deployment for application abc123 with version 2.1.0
```

---

### `deployment_get_latest`

Get the most recent deployment for an application along with its error groups.

**Parameters:**
- `appId` (string, required): The unique identifier of the Raygun application
- `maxErrorGroups` (integer, optional): Maximum number of error groups to include (default: 50, max: 200)

**Example:**
```
Show me the latest deployment and any errors for application abc123
```

---

### `deployment_investigate`

Get comprehensive information about a specific deployment including details and related error groups.

**Parameters:**
- `appId` (string, required): The unique identifier of the Raygun application
- `deploymentId` (string, required): The unique identifier of the deployment
- `maxErrorGroups` (integer, optional): Maximum number of error groups to include (default: 50, max: 200)

**Example:**
```
Investigate deployment def456 in application abc123
```

---

### `deployment_manage`

Update or delete a deployment record.

**Parameters:**
- `appId` (string, required): The unique identifier of the Raygun application
- `deploymentId` (string, required): The unique identifier of the deployment
- `action` (string, required): Action to perform: `update` or `delete`
- `updateData` (object, optional): Updated deployment information (required for update action):
  - `Version` (string, optional)
  - `DeployedAt` (datetime, optional)
  - `OwnerName` (string, optional)
  - `EmailAddress` (string, optional)
  - `Comment` (string, optional)
  - `ScmType` (string, optional)
  - `ScmIdentifier` (string, optional)

**Example:**
```
Update deployment def456 to add comment "Hotfix for authentication issue"
```

---

## Customers & Sessions

### `customers_search`

Search for customers in a Raygun application by name, email address, or unique identifier. Returns matching customers with their internal Identifier (base36), which is needed to pass to `customer_investigate`. Use this tool to look up a customer's internal Identifier when you only have their external identifier (e.g. an email address or SDK-provided user ID like "12800").

**Parameters:**
- `appId` (string, required): The unique identifier of the Raygun application (base36)
- `searchTerm` (string, required): Search term to match against customer first name, full name, email address, or unique identifier
- `count` (integer, optional): Maximum number of customers to return (default: 100, max: 500)

**Example:**
```
Search for customer "user@example.com" in application abc123
```

---

### `customer_investigate`

Get a customer's profile, recent error groups (with instance counts and messages), and recent sessions. The `customerId` parameter expects the internal Identifier (base36) returned by `customers_search` — not the customer's external identifier (e.g. email or SDK-provided user ID). Use `customers_search` first to find the internal Identifier for a customer.

**Returns:**
- **Customer profile**: name, email, external identifier, location, first/last seen
- **Recent error groups**: up to 20 most recent error groups, each with message, instance count, and first/last occurred timestamps
- **Recent sessions**: up to 10 most recent sessions, each with browser, version, start/end times, active status

**Parameters:**
- `appId` (string, required): The unique identifier of the Raygun application (base36)
- `customerId` (string, required): The customer's internal Identifier (base36) returned by `customers_search`
- `startTime` (string, optional): Start of the time range for errors and sessions (ISO 8601, e.g. '2024-01-15T00:00:00Z'). Defaults to 30 days ago.
- `endTime` (string, optional): End of the time range for errors and sessions (ISO 8601, e.g. '2024-02-15T00:00:00Z'). Defaults to now.

**Example:**
```
Search for customer "user@example.com" in application abc123, then investigate their recent errors and sessions using the returned Identifier
```

---

### `sessions_list`

List user sessions to analyze user behavior, environment data, and device information.

**Parameters:**
- `appId` (string, required): The unique identifier of the Raygun application
- `count` (integer, optional): Maximum number of sessions to return (default: 100, max: 500)
- `offset` (integer, optional): Number of sessions to skip for pagination (0-based)
- `filterExpression` (string, optional): Filter expression. Examples: `countryCode = "US"`, `browserName = "Chrome"`
- `sortOrder` (string, optional): Sort order. Available fields: `startedAt`, `updatedAt`, `endedAt`, `customerIdentifier`, `countryCode`, `platformName`, `operatingSystemName`, `browserName`

**Example:**
```
List recent sessions from the US using Chrome
```

---

## Performance & Metrics

### `pages_list`

List pages in a Raygun application to get page identifiers for metrics queries.

**Parameters:**
- `appId` (string, required): The unique identifier of the Raygun application
- `count` (integer, optional): Maximum number of pages to return (default: 100, max: 500)
- `offset` (integer, optional): Number of pages to skip for pagination (0-based)
- `sortOrder` (string, optional): Sort order. Available fields: `identifier`, `lastSeenAt`, `uri`. Examples: `lastSeenAt desc`

**Example:**
```
List monitored pages for application abc123
```

---

### `page_investigate`

Get basic information about a specific page (ID, URL/name, last seen).

**Parameters:**
- `appId` (string, required): The unique identifier of the Raygun application
- `pageId` (string, required): The unique identifier of the page

**Example:**
```
Get details for page page123
```

---

### `metrics_website_performance_analyze`

Analyze website performance metrics as time-series data to track trends and monitor improvements.

**Parameters:**
- `appId` (string, required): The unique identifier of the Raygun application
- `startTime` (datetime, required): Start date and time (ISO 8601 format, e.g., `2024-01-15T00:00:00Z`)
- `endTime` (datetime, required): End date and time (ISO 8601 format, max 30 days from start)
- `metrics` (array, required): Performance metrics to analyze: `loadTime`, `firstPaint`, `firstContentfulPaint`, `firstInputDelay`, `pageViews`
- `granularity` (string, optional): Data granularity: `15m`, `1h`, `4h`, `12h`, `1d`, `7d` (default: `1h`)
- `aggregation` (string, optional): Statistical method: `average`, `median`, `p95`, `p99` (default: `average`)
- `filter` (string, optional): Filter by pages. Examples: `pageIdentifier = abc123`

**Example:**
```
Show me page load times for the last 7 days with daily granularity
```

---

### `metrics_performance_distribution_analyze`

Analyze performance metrics as histogram data to understand user experience distribution.

**Parameters:**
- `appId` (string, required): The unique identifier of the Raygun application
- `startTime` (datetime, required): Start date and time (ISO 8601 format)
- `endTime` (datetime, required): End date and time (ISO 8601 format, max 7 days)
- `metrics` (array, required): Performance metrics: `loadTime`, `firstPaint`, `firstContentfulPaint`, `firstInputDelay`
- `filter` (string, optional): Filter by pages

**Example:**
```
Show me the distribution of load times over the last 24 hours
```

---

### `metrics_error_trends_analyze`

Analyze error metrics as time-series data to track error trends and monitor application reliability.

**Parameters:**
- `appId` (string, required): The unique identifier of the Raygun application
- `startTime` (datetime, required): Start date and time (ISO 8601 format)
- `endTime` (datetime, required): End date and time (ISO 8601 format, max 90 days)
- `metrics` (array, required): Error metrics: `errorInstances`
- `granularity` (string, optional): Data granularity: `15m`, `1h`, `4h`, `12h`, `1d`, `7d` (default: `1h`)
- `aggregation` (string, optional): Statistical method: `count`, `average`, `sum` (default: `count`)
- `filter` (string, optional): Filter by error groups. Examples: `errorGroupIdentifier = abc123`

**Example:**
```
Show me error trends for the last 30 days
```

---

## Team Management

### `invitations_manage`

List and review team invitations to manage user access and onboarding.

**Parameters:**
- `count` (integer, optional): Maximum number of invitations to return (default: 100, max: 500)
- `offset` (integer, optional): Number of invitations to skip for pagination (0-based)
- `invitationId` (string, optional): Specific invitation ID to get detailed information
- `sortOrder` (string, optional): Sort order. Available fields: `identifier`, `emailAddress`, `createdAt`, `status`. Examples: `createdAt desc`

**Example:**
```
List all pending team invitations
```

---

### `invitation_send`

Send a team invitation to grant Raygun access to a new user.

**Parameters:**
- `emailAddress` (string, required): Email address of the person to invite

**Example:**
```
Send an invitation to newuser@example.com
```

---

### `invitation_revoke`

Cancel a pending team invitation that has not yet been accepted.

**Parameters:**
- `invitationId` (string, required): The unique identifier of the invitation to revoke

**Example:**
```
Revoke invitation inv123
```
