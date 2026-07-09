---
type: Web Page
title: Core Backend Service APIs | Backstage Software Catalog and Developer Platform
description: Core backend service APIs
resource: https://backstage.io/docs/backend-system/core-services/index
timestamp: '2026-07-09T12:16:50.465553+00:00'
---

# Core Backend Service APIs

The default backend provides several [core services](https://github.com/backstage/backstage/blob/master/packages/backend-plugin-api/src/services/definitions/coreServices.ts) out of the box which includes access to configuration, logging, URL Readers, databases and more.

All core services are available through the `coreServices` namespace in the `@backstage/backend-plugin-api` package:

```
import { coreServices } from '@backstage/backend-plugin-api';
```
## Service Documentation Index

- [Auth Service](/docs/backend-system/core-services/auth)- Token authentication and credentials management.
- [Cache Service](/docs/backend-system/core-services/cache)- Key-value store for caching data.
- [Database Service](/docs/backend-system/core-services/database)- Database access and management via- [knex](https://knexjs.org/).
- [Discovery Service](/docs/backend-system/core-services/discovery)- Service discovery for inter-plugin communication.
- [Http Auth Service](/docs/backend-system/core-services/http-auth)- Authentication of HTTP requests.
- [Http Router Service](/docs/backend-system/core-services/http-router)- HTTP route registration for plugins.
- [Identity Service](/docs/backend-system/core-services/identity)- Deprecated user authentication service, use the- [Auth Service](/docs/backend-system/core-services/auth)instead.
- [Lifecycle Service](/docs/backend-system/core-services/lifecycle)- Registration of plugin startup and shutdown lifecycle hooks.
- [Logger Service](/docs/backend-system/core-services/logger)- Plugin-level logging.
- [Metrics Service](/docs/backend-system/core-services/metrics)- Plugin-scoped metrics instrumentation (alpha).
- [Permissions Service](/docs/backend-system/core-services/permissions)- Permission system integration for authorization of user actions.
- [Plugin Metadata Service](/docs/backend-system/core-services/plugin-metadata)- Built-in service for accessing metadata about the current plugin.
- [Root Config Service](/docs/backend-system/core-services/root-config)- Access to static configuration.
- [Root Health Service](/docs/backend-system/core-services/root-health)- Health check endpoints for the backend.
- [Root Http Router Service](/docs/backend-system/core-services/root-http-router)- HTTP route registration for root services.
- [Root Lifecycle Service](/docs/backend-system/core-services/root-lifecycle)- Registration of backend startup and shutdown lifecycle hooks.
- [Root Logger Service](/docs/backend-system/core-services/root-logger)- Root-level logging.
- [Scheduler Service](/docs/backend-system/core-services/scheduler)- Scheduling of distributed background tasks.
- [Token Manager Service](/docs/backend-system/core-services/token-manager)- Deprecated service authentication service, use the- [Auth Service](/docs/backend-system/core-services/auth)instead.
- [Tracing Service](/docs/backend-system/core-services/tracing)- Plugin-scoped trace span emission with built-in principal enrichment (alpha).
- [Url Reader Service](/docs/backend-system/core-services/url-reader)- Reading content from external systems.
- [User Info Service](/docs/backend-system/core-services/user-info)- Authenticated user information retrieval.

# Citations

1. Source page: https://backstage.io/docs/backend-system/core-services/index
