---
type: Web Page
title: Integrate into the Software Catalog | Backstage Software Catalog and Developer
  Platform
description: How to integrate a plugin into software catalog
resource: https://backstage.io/docs/plugins/integrating-plugin-into-software-catalog
timestamp: '2026-07-06T13:23:17.605783+00:00'
---

# Integrate into the Software Catalog

This page describes integrating plugins into the Software Catalog using the **old frontend system** patterns (`EntitySwitch`, `EntityLayout`, `EntityLayout.Route`). For the new frontend system, entity page integrations are done using `EntityCardBlueprint` and `EntityContentBlueprint` — see Common Extension Blueprints.

This is an advanced use case and currently is an experimental feature. Expect API to change over time

## Steps

- Create a plugin
- Reading entities from within your plugin
- Import your plugin and embed in the entities page

### Create a plugin

Follow the same process as for standalone plugin. You should have a separate package in a folder, which represents your plugin.

Example:

```
$ yarn new
# Select `frontend-plugin`
> ? Enter an ID for the plugin [required] my-plugin
> ? Enter the owner(s) of the plugin. If specified, this will be added to CODEOWNERS for the plugin path. [optional]
Creating the plugin...
```
### Reading entities from within your plugin

You can access the currently selected entity using the backstage api
`useEntity`. For example,

```
import { useEntity } from '@backstage/plugin-catalog-react';
export const MyPluginEntityContent = () => {
  const entity = useEntity();
  // Do something with the entity data...
};
```
Internally `useEntity` makes use of
react `Contexts`. The entity context is
provided by the entity page into which your plugin will be embedded.

### Import your plugin and embed in the entities page

To begin, you will need to import your plugin in the entities page. Located at
`packages/app/src/components/Catalog/EntityPage.tsx` from the root package of
your backstage app.

```
import { MyPluginEntityContent } from '@backstage/plugin-my-plugin';
```
To add your component to the Entity view, you will need to modify the
`packages/app/src/components/Catalog/EntityPage.tsx`. Depending on the needs of
your plugin, you may only care about certain kinds of
entities,
each of which has its own
element for rendering. This
functionality is handled by the `EntitySwitch` component:

```
export const entityPage = (
  <EntitySwitch>
    <EntitySwitch.Case if={isKind('component')} children={componentPage} />
    <EntitySwitch.Case if={isKind('api')} children={apiPage} />
    <EntitySwitch.Case if={isKind('group')} children={groupPage} />
    <EntitySwitch.Case if={isKind('user')} children={userPage} />
    <EntitySwitch.Case if={isKind('system')} children={systemPage} />
    <EntitySwitch.Case if={isKind('domain')} children={domainPage} />
    <EntitySwitch.Case>{defaultEntityPage}</EntitySwitch.Case>
  </EntitySwitch>
);
```
At this point, you will need to modify the specific page where you want your
component to appear. If you are extending the Software Catalog model you will
need to add a new case to the `EntitySwitch`. For adding a plugin to an existing
component type, you modify the existing page. For example, if you want to add
your plugin to the `systemPage`, you can add a new tab by adding an
`EntityLayout.Route` such as below:

```
const systemPage = (
  <EntityLayout>
    <EntityLayout.Route path="/" title="Overview">
      <Grid container spacing={3} alignItems="stretch">
        <Grid item md={6}>
          <EntityAboutCard />
        </Grid>
        <Grid item md={6}>
          <EntityHasComponentsCard variant="gridItem" />
        </Grid>
        <Grid item md={6}>
          <EntityHasApisCard variant="gridItem" />
        </Grid>
        <Grid item md={6}>
          <EntityHasResourcesCard variant="gridItem" />
        </Grid>
      </Grid>
    </EntityLayout.Route>
    <EntityLayout.Route path="/diagram" title="Diagram">
      <EntityCatalogGraphCard variant="gridItem" height={400} />
    </EntityLayout.Route>
    {/* Adding a new tab to the system view */}
    <EntityLayout.Route path="/your-custom-route" title="CustomTitle">
      <MyPluginEntityContent />
    </EntityLayout.Route>
  </EntityLayout>
);
```

# Citations

1. Source page: https://backstage.io/docs/plugins/integrating-plugin-into-software-catalog
