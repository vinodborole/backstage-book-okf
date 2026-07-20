---
type: Web Page
title: Filtering the Catalog | Backstage Software Catalog and Developer Platform
description: Filtering the Catalog.
resource: https://backstage.io/docs/getting-started/filter-catalog
timestamp: '2026-07-20T08:58:01.906190+00:00'
---

# Filtering the Catalog

Audience: All

## Overview

The Catalog can be filtered by any combination of owner, kind, type, lifecycle, processing status, namespace, and name. [Catalog filters](/docs/features/software-catalog/catalog-customization#catalog-filters) provides information on how to modify the available filter criteria.

The [Technical Overview](/docs/overview/technical-overview#software-catalog-system-model) provides a description of the types of entities displayed in the Catalog.

## Filtering the Catalog

You can filter the Catalog using a combination of the following:

- 
**Filter by name**Enter one or more consecutive letters into the `Filter`field. As you type the letters, the entities whose names do not contain that string will be filtered out of the displayed list.
- 
**Filter by kind**Use the `Kind`dropdown list to select which kind of entity to show in the list:- API
- Component
- Group
- Location
- System
- Template
- User
 
- 
**Filter by Type**Use the `Type`dropdown list to select which type of entity to show in the list. The selections available in the dropdown list depend on the kind of entity selected in the`Kind`list, and the types of entity you have registered for that kind.
- 
**Filter by Owner**Use the `Owner`dropdown to filter the Catalog list by who owns the entity.
- 
**Filter by Lifecycle**Use the `Lifecycle`dropdown to filter the Catalog list by lifecycle.
- 
**Filter by Processing Status**Use the `Processing Status`dropdown to restrict the displayed list to only include those entities which are[orphaned](/docs/features/software-catalog/life-of-an-entity#orphaning)or[in error](/docs/features/software-catalog/life-of-an-entity#errors).
- 
**Filter by Namespace**Use the `Namespace`dropdown to filter the catalog list by namespace associated with the entity.

# Citations

1. Source page: https://backstage.io/docs/getting-started/filter-catalog
