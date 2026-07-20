---
type: Web Page
title: Deploying Backstage | Backstage Software Catalog and Developer Platform
description: Packaging Backstage and deploying to production
resource: https://backstage.io/docs/deployment
timestamp: '2026-07-20T08:58:01.906190+00:00'
---

# Deploying Backstage

Backstage provides tooling to build Docker images, but can be deployed with or
without Docker on many different infrastructures. The *best* way to deploy
Backstage is in *the same way* you deploy other software at your organization.

This documentation shows common examples that may be useful when deploying Backstage for the first time, or for those without established deployment practices.

The *easiest* way to explore Backstage is to visit the
[live demo site](https://demo.backstage.io).

At Spotify, we deploy software generally by:

- Building a Docker image
- Storing the Docker image on a container registry
- Referencing the image in a Kubernetes Deployment YAML
- Applying that Deployment to a Kubernetes cluster

This method is covered in [Building a Docker image](/docs/deployment/docker) and
[Deploying with Kubernetes](/docs/deployment/k8s).

There are many ways to deploy Backstage! You can find more examples in the community contributed guides found [here](https://github.com/backstage/backstage/blob/master/contrib/docs/tutorials/).

If you need to run Backstage behind a corporate proxy, see the [corporate proxy guide](/docs/tutorials/corporate-proxy).

# Citations

1. Source page: https://backstage.io/docs/deployment
