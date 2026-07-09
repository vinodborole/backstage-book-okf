---
type: Web Page
title: Backstage Software Catalog | Backstage Software Catalog and Developer Platform
description: The Backstage Software Catalog
resource: https://backstage.io/docs/features/software-catalog
timestamp: '2026-07-09T12:16:50.465553+00:00'
---

# Backstage Software Catalog

## What is a Software Catalog?

The Backstage Software Catalog is a centralized system that keeps track of
ownership and metadata for all the software in your ecosystem (services,
websites, libraries, data pipelines, etc). The catalog is built around the
concept of [metadata YAML files](/docs/features/software-catalog/descriptor-format) stored together with the
code, which are then harvested and visualized in Backstage.

## How it works

Backstage and the Backstage Software Catalog make it easy for one team to manage 10 services — and makes it possible for your company to manage thousands of them.

More specifically, the Software Catalog enables two main use-cases:

- Helping teams manage and maintain the software they own. Teams get a uniform view of all their software; services, libraries, websites, ML models — you name it, Backstage knows all about it.
- Makes all the software in your company, and who owns it, discoverable. No more orphan software hiding in the dark corners of your software ecosystem.

## Getting Started

The Software Catalog is available to browse at `/catalog`. If you've followed
[Getting Started with Backstage](/docs/getting-started/), you should be able to
browse the catalog at `http://localhost:3000`.

## Adding components to the catalog

The source of truth for the components in your software catalog are [metadata YAML files](/docs/features/software-catalog/descriptor-format) stored in source control (GitHub, GitHub
Enterprise, GitLab, ...). Repositories can include one or multiple metadata
files. Usually the metadata file is located in the repository root. This is not
a formal requirement & metadata files can be placed anywhere in the repository.

There are 3 ways to add components to the catalog:

- Manually register components
- Creating new components through Backstage
- Integrating with an [external source](/docs/features/software-catalog/external-integrations)

### Manually register components

Users can register new components by going to `/create` and clicking the
**REGISTER EXISTING COMPONENT** button:

Backstage expects the full URL to the YAML in your source control. Example:

```
https://github.com/backstage/backstage/blob/master/packages/catalog-model/examples/components/artist-lookup-component.yaml
```
*More examples can be found
 here.*

It is important to note that any kind of software can be registered in Backstage. Even if the software is not maintained by your company (SaaS offering, for example) it is still useful to create components for tracking ownership.

### Creating new components through Backstage

All software created through the
[Backstage Software Templates](/docs/features/software-templates/) are automatically
registered in the catalog.

### Static catalog configuration

In addition to manually registering components, it is also possible to register
components through [static configuration](/docs/conf/). For example, the
above example can be added using the following configuration:

```
catalog:
  locations:
    - type: url
      target: https://github.com/backstage/backstage/blob/master/packages/catalog-model/examples/components/artist-lookup-component.yaml
```
More information about catalog configuration can be found
[here](/docs/features/software-catalog/configuration).

### Updating component metadata

Teams owning the components are responsible for maintaining the metadata about them, and do so using their normal Git workflow.

Once the change has been merged, Backstage will automatically show the updated metadata in the software catalog after a short while.

## Finding software in the catalog

By default, the software catalog shows components owned by the team of the logged
in user. But you can also switch to *All* to see all the components across your
company's software ecosystem. Basic inline *search* and *column filtering* makes
it easy to browse a big set of components.

## Starring components

For easy and quick access to components you visit frequently, Backstage supports
*starring* of components:

## Integrated tooling through plugins

The software catalog is a great way to organize the infrastructure tools you use to manage the software. This is how Backstage creates one developer portal for all your tools. Rather than asking teams to jump between different infrastructure user interfaces (and incurring additional cognitive overhead each time they make a context switch), most of these tools can be organized around the entities in the catalog.

Your Backstage developer portal can be customized by incorporating
[existing open source plugins](https://github.com/backstage/backstage/tree/master/plugins),
or by [building your own](/docs/plugins/).

## Unprocessed Entities

Sometimes entities fail to process correctly. The **Unprocessed Entities** feature helps Backstage admins find and diagnose these entities to understand the state of the catalog.

To use this feature, check out the documentation for the [catalog-unprocessed-entities plugin](https://github.com/backstage/backstage/tree/master/plugins/catalog-unprocessed-entities) and its [backend module](https://github.com/backstage/backstage/tree/master/plugins/catalog-backend-module-unprocessed).

# Citations

1. Source page: https://backstage.io/docs/features/software-catalog
