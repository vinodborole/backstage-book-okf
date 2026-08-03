---
type: Web Page
title: Deploying Backstage | Backstage Software Catalog and Developer Platform
description: Packaging Backstage and deploying to production
resource: https://backstage.io/docs/deployment
timestamp: '2026-08-03T09:44:12.848210+00:00'
---

# Deploying Backstage

Backstage provides tooling to build Docker images, but can be deployed with or
without Docker on many different infrastructures. The *best* way to deploy
Backstage is in *the same way* you deploy other software at your organization.

This documentation shows common examples that may be useful when deploying Backstage for the first time, or for those without established deployment practices.

The *easiest* way to explore Backstage is to visit the
[live demo site](https://demo.backstage.io).

At Spotify, we deploy software generally by:

1. Building a Docker image
2. Storing the Docker image on a container registry
3. Referencing the image in a Kubernetes Deployment YAML
4. Applying that Deployment to a Kubernetes cluster

This method is covered in [Building a Docker image](/docs/deployment/docker) and
[Deploying with Kubernetes](/docs/deployment/k8s).

There are many ways to deploy Backstage! You can find more examples in the community contributed guides found [here](https://github.com/backstage/backstage/blob/master/contrib/docs/tutorials/).

If you need to run Backstage behind a corporate proxy, see the [corporate proxy guide](/docs/tutorials/corporate-proxy).

# Citations

1. Source page: https://backstage.io/docs/deployment
