---
type: Web Page
title: Integrations | Backstage Software Catalog and Developer Platform
description: Configuring Backstage to read or publish data with external providers
  using integrations
resource: https://backstage.io/docs/integrations
timestamp: '2026-07-06T13:23:17.605783+00:00'
---

# Integrations

Integrations allow Backstage to read or publish data using external providers such as GitHub, GitLab, Bitbucket, LDAP, or cloud providers.

## Configuration

Integrations are configured at the root level of `app-config.yaml` since
integrations are used by many Backstage core features and other plugins.

Each key under `integrations` is a separate configuration for a single external
provider. Providers each have different configuration; here's an example of
configuration to use GitHub:

```
integrations:
  github:
    - host: github.com
      token: ${GITHUB_TOKEN}
```
See documentation for each type of integration for full details on configuration.

# Citations

1. Source page: https://backstage.io/docs/integrations
