---
type: Web Page
title: Viewing the Catalog | Backstage Software Catalog and Developer Platform
description: Viewing the Catalog
resource: https://backstage.io/docs/getting-started/viewing-catalog
timestamp: '2026-07-20T08:58:01.906190+00:00'
---

# Viewing the Catalog

Audience: All

## Overview

Initially, when you log into your standalone Backstage App, `Home` is selected in the sidebar, which displays the Catalog in the main panel.

There are four main entities that you should become familiar with:

- `Components`- Individual pieces of software that can be tracked in source control and can implement APIs for other components to consume.
- `Resources`- The physical or virtual infrastructure needed to operate a component.
- `Systems`- A collection of resources and components that cooperate to perform a function by exposing one or several public APIs. It hides the resources and private APIs between the components from the consumer.
- `Domains`- A collection of systems that share terminology, domain models, metrics, KPIs, business purpose, or documentation.

The [Technical Overview](/docs/overview/technical-overview#software-catalog-system-model) provides a description of all of the types of entities displayed in the Catalog.

It should be noted that you can also [create your own kinds of entities](/docs/features/software-catalog/extending-the-model#adding-a-new-kind), if you need to model something in your organization that does not map to one of the existing entity types.

Initially, the Catalog displays registered entities matching the following filter settings:

- `Kind`- Component
- `Type`- all
- `Owner`- Owned
- `Lifecycle`- list of- [lifecycle](/docs/features/software-catalog/descriptor-format#speclifecycle-required)values of entities in the Catalog
- `Processing Status`- normal
- `Namespace`- The ID of a- [namespace](/docs/features/software-catalog/descriptor-format#namespace-optional)to which the entity belongs

You can change the initial setting for the [Owner](/docs/features/software-catalog/catalog-customization#catalog-filters) and [Kind](/docs/features/software-catalog/catalog-customization#catalog-filters) filters.

## Informational columns for each entity

For each kind of entity, a set of columns display information regarding the entity. For example, the default set of information for a `Component` is:

- `Name`- the name of the component
- `System`- an optional field that references the system to which the component belongs
- `Owner`- the owner of the component
- `Type`- common types are as follows, but you can- [create a new type](/docs/features/software-catalog/extending-the-model#adding-a-new-type-of-an-existing-kind)to meet your organization's needs- `service`- a backend service, typically exposing an API
- `website`- a website
- `library`- a software library, such as an npm module or a Java library
 
- `Lifecycle`- `experimental`- an experiment or early, non-production component, signaling that users may not prefer to consume it over other more established components, or that there are low or no reliability guarantees
- `production`- an established, owned, maintained component
- `deprecated`- a component that is at the end of its lifecycle, and may disappear at a later point in time
 
- `Description`- an optional field that describes the component.
- `Tags`- an optional field that can be used for searching
- `Actions`- see- [Catalog Actions](#catalog-actions)

You can modify the columns associated with each kind of entity, following the instructions in [Customizing columns, actions, and table options](/docs/features/software-catalog/catalog-customization#customizing-columns-actions-and-table-options).

## Catalog Actions

For each entity, there are a set of actions that are available.

From left to right, the actions are:

- View - View the `catalog-info.yaml`file that defines the entity.
- Edit - Edit the `catalog-info.yaml`file that defines the entity. See[Updating a Component](/docs/getting-started/update-a-component)
- Star - Designate the entity as a favorite. You can [filter](/docs/getting-started/filter-catalog)the catalog for starred entities.

[Customizing columns, actions, and table options](/docs/features/software-catalog/catalog-customization#customizing-columns-actions-and-table-options) describes how you can modify the actions that are displayed.

## Viewing entity details

Selecting an entity in the main panel displays details of the entity. The type of details depends on the type of entity. For example, selecting a Component, such as `example-website`, displays the following details:

- `About`- Metadata for the entity, such as description, owner, tags, and domain.
- `Relations`- see- [Viewing entity relationships](/docs/getting-started/viewing-entity-relationships)
- `Links`- any links associated with the entity
- `Has subcomponents`- An entity reference to another component of which the component is a part

Selecting a System, such as `examples`, displays `About`, `Relations`, and `Links` similar to a Component, but it also includes `Has components`, `APIs` and `Has Resources`.

# Citations

1. Source page: https://backstage.io/docs/getting-started/viewing-catalog
