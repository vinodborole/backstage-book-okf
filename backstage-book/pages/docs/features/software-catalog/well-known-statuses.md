---
type: Web Page
title: Well-known Status fields of Catalog Entities | Backstage Software Catalog and
  Developer Platform
description: Lists a number of well known entity statuses, that have defined semantics.
  They can be attached to catalog entities and consumed by plugins as needed.
resource: https://backstage.io/docs/features/software-catalog/well-known-statuses
timestamp: '2026-07-06T13:23:17.605783+00:00'
---

# Well-known Status fields of Catalog Entities

This section lists well known entity statuses, that have defined semantics. They can be attached to catalog entities and consumed by plugins as needed.

If you are looking to extend the statuses, see Extending the model.

## Common Fields

The `status` object of an entity is currently left unrestricted, except for the
`items` field. Its structure is defined in the
descriptor format section.

We reserve the right to extend this model in the future. This status is in active development and its format will change unexpectedly. Do not consume it in your own code until such a time that this documentation has been updated.

## Status Item Types

This is a (non-exhaustive) list of `status.items.[].type` values that are known
to be in active use.

`backstage.io/catalog-processing`

Expresses an aspect of the current status of the catalog's ingestion of this entity. Errors that may appear here include inability to read from the remote SCM provider, syntax errors in the YAML file, and similar.

Note that the entity data itself may be of an older version, when errors are present. The ingestion system keeps the old valid entity data untouched when possible, so the errors described in this state may not seem to align with the rest of the entity, because they pertain to a remote that could not be successfully ingested. This is normal.

```
# Example:
status:
  items:
    - type: backstage.io/catalog-processing
      level: error
      message: 'NotFoundError: File not found'
      error:
        name: NotFoundError
        message: File not found
        stack: ...
```

# Citations

1. Source page: https://backstage.io/docs/features/software-catalog/well-known-statuses
