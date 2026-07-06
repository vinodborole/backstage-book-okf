---
type: Web Page
title: Core Backend Service APIs | Backstage Software Catalog and Developer Platform
description: Core backend service APIs
resource: https://backstage.io/docs/backend-system/core-services/index
timestamp: '2026-07-06T13:23:17.605783+00:00'
---

# Core Backend Service APIs

The default backend provides several core services out of the box which includes access to configuration, logging, URL Readers, databases and more.

All core services are available through the `coreServices` namespace in the `@backstage/backend-plugin-api` package:

```
import { coreServices } from '@backstage/backend-plugin-api';
```
## Service Documentation Index

- Auth Service - Token authentication and credentials management.
- Cache Service - Key-value store for caching data.
- Database Service - Database access and management via knex.
- Discovery Service - Service discovery for inter-plugin communication.
- Http Auth Service - Authentication of HTTP requests.
- Http Router Service - HTTP route registration for plugins.
- Identity Service - Deprecated user authentication service, use the Auth Service instead.
- Lifecycle Service - Registration of plugin startup and shutdown lifecycle hooks.
- Logger Service - Plugin-level logging.
- Metrics Service - Plugin-scoped metrics instrumentation (alpha).
- Permissions Service - Permission system integration for authorization of user actions.
- Plugin Metadata Service - Built-in service for accessing metadata about the current plugin.
- Root Config Service - Access to static configuration.
- Root Health Service - Health check endpoints for the backend.
- Root Http Router Service - HTTP route registration for root services.
- Root Lifecycle Service - Registration of backend startup and shutdown lifecycle hooks.
- Root Logger Service - Root-level logging.
- Scheduler Service - Scheduling of distributed background tasks.
- Token Manager Service - Deprecated service authentication service, use the Auth Service instead.
- Tracing Service - Plugin-scoped trace span emission with built-in principal enrichment (alpha).
- Url Reader Service - Reading content from external systems.
- User Info Service - Authenticated user information retrieval.

# Citations

1. Source page: https://backstage.io/docs/backend-system/core-services/index
