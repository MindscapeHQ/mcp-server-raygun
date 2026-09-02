# Raygun MCP Tools

The Raygun MCP server exposes the tools below. Your MCP client receives the current parameter and response schemas directly from the server, so it can select and call tools without manually constructed API requests.

Tool availability depends on the scopes approved during OAuth authorization or assigned to your Personal Access Token.

## Applications

- `applications_list` — List applications available to the current user.
- `applications_search` — Find applications by name.
- `application_get_details` — Get an application's product-data status and plan information, optionally including its ingestion API key.
- `application_regenerate_api_key` — Rotate an application's ingestion API key. The previous key stops working immediately.

## Error Management

- `error_groups_list` — List error-group metadata for an application.
- `error_groups_search` — Search indexed occurrences across messages, exception types, stack traces, URLs, hosts, versions, tags, custom data, breadcrumbs, machines, and affected users.
- `error_group_investigate` — Inspect an error group and its latest occurrence, including typed error or CSP violation details and request context.
- `error_group_instances_list` — List occurrence identifiers and timestamps for an error group.
- `error_instance_get` — Get full typed details for one occurrence, including its exception graph or CSP violation, request context, environment, and breadcrumbs.
- `error_group_update_status` — Activate, resolve, ignore, or permanently ignore an error group.
- `error_group_add_comment` — Add an investigation or collaboration note to an error group.
- `error_group_read_comments` — Read existing comments on an error group.

## Application Performance Monitoring

- `apm_issues_search` — Find recurring performance issues and anti-patterns such as slow methods, slow queries, chatty APIs, and N+1 queries.
- `apm_issue_investigate` — Inspect an APM issue's metric, percentiles, and recent affected traces.
- `apm_traces_search` — Find traces by time, request text, duration, or status code.
- `apm_trace_investigate` — Inspect a trace's summary, profiler threads, linked issues, and most significant calls.
- `apm_hotspots_search` — Rank methods, database queries, or external calls by average duration, total duration, or call count.

## Deployments

- `deployments_list` — Browse deployment history for an application.
- `deployment_get_latest` — Get the most recent deployment and its related error groups.
- `deployment_investigate` — Inspect a deployment and errors associated with that release.
- `deployment_create` — Record a deployment using an application identifier or ingestion API key.
- `deployment_manage` — Update deployment metadata or delete an incorrectly created deployment.

## Customers and Sessions

- `customers_search` — Find customers by name, email address, or external identifier.
- `customer_investigate` — Get a customer profile, recent error groups, and recent sessions. Use the internal identifier returned by `customers_search`.
- `sessions_list` — List sessions with timing, location, browser, operating system, viewport, and deployment information.
- `session_investigate` — Inspect a session's environment, errors, and page-view journey.

## Pages and Metrics

- `pages_list` — List monitored pages for use in session and performance queries.
- `page_investigate` — Get a page's identifier, URL or name, type, and last-seen time.
- `metrics_website_performance_analyze` — Analyze page performance as a time series using average, median, p95, or p99 aggregation.
- `metrics_performance_distribution_analyze` — Analyze performance as histogram buckets to understand user-experience distribution and outliers.
- `metrics_error_trends_analyze` — Analyze error counts, affected users, and affected sessions over time.

## Team Invitations

- `invitations_manage` — List and review team invitations.
- `invitation_send` — Invite a user and grant access to selected applications.
- `invitation_revoke` — Revoke a pending invitation.

## Suggested Workflows

### Investigate an error

1. Use `applications_search` to find the application.
2. Use `error_groups_search` to locate the symptom, or `error_groups_list` to browse groups.
3. Use `error_group_investigate` for the current failure and request context.
4. Use `error_group_instances_list` and `error_instance_get` to compare exact occurrences.
5. Review or add investigation notes with `error_group_read_comments` and `error_group_add_comment`.

### Investigate backend performance

1. Use `apm_issues_search` or `apm_hotspots_search` to identify recurring bottlenecks.
2. Use `apm_issue_investigate` to review percentiles and affected traces.
3. Use `apm_trace_investigate` to inspect the significant calls in a representative trace.

### Investigate a user's experience

1. Use `customers_search` and pass its internal customer identifier to `customer_investigate`.
2. Use `session_investigate` to inspect the user's environment, errors, and page journey.
3. Use `error_group_investigate` or `error_instance_get` for the underlying failure.

### Assess a release

1. Use `deployment_get_latest` or `deployments_list` to find the release.
2. Use `deployment_investigate` to review associated errors.
3. Use `metrics_error_trends_analyze` and APM tools to compare reliability and performance around the deployment.
