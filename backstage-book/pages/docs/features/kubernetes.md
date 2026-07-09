---
type: Web Page
title: Kubernetes | Backstage Software Catalog and Developer Platform
description: Monitoring Kubernetes based services with the software catalog
resource: https://backstage.io/docs/features/kubernetes
timestamp: '2026-07-09T12:16:50.465553+00:00'
---

# Kubernetes

Kubernetes in Backstage is a tool that's designed around the needs of service owners, not cluster admins. Now developers can easily check the health of their services no matter how or where those services are deployed — whether it's on a local host for testing or in production on dozens of clusters around the world.

It will elevate the visibility of errors where identified, and provide drill down about the deployments, pods, and other objects for a service.

The feature is made up of two plugins:
[ @backstage/plugin-kubernetes](https://github.com/backstage/backstage/tree/master/plugins/kubernetes)
and

[.](https://github.com/backstage/backstage/tree/master/plugins/kubernetes-backend)

`@backstage/plugin-kubernetes-backend`The frontend plugin exposes information to the end user in a digestible way, while the backend wraps the mechanics to connect to Kubernetes clusters to collect the relevant information.

## Let's use it!

To get started, first you must [install the Kubernetes plugins](/docs/features/kubernetes/installation)
and then [configure them](/docs/features/kubernetes/configuration).

# Citations

1. Source page: https://backstage.io/docs/features/kubernetes
