---
type: Web Page
title: Plugin Development | Backstage Software Catalog and Developer Platform
description: Documentation on Plugin Development
resource: https://backstage.io/docs/plugins/plugin-development
timestamp: '2026-07-06T13:23:17.605783+00:00'
---

# Plugin Development

This page covers plugin development patterns for the **old frontend system**, including `createPlugin`, `createRoutableExtension`, and `RouteRef` from `@backstage/core-plugin-api`. For the new frontend system equivalents, see Building Frontend Plugins and Routes.

Backstage plugins provide features to a Backstage App.

Each plugin is treated as a self-contained web app and can include almost any type of content. Plugins all use a common set of platform APIs and reusable UI components. Plugins can fetch data from external sources using the regular browser APIs or by depending on external modules to do the work.

## Developing guidelines

- Consider writing plugins in `TypeScript`.
- Plan the directory structure of your plugin so that it becomes easy to manage.
- Prefer using the Backstage components, otherwise go with Material UI.
- Check out the shared Backstage APIs before building a new one.

## Plugin concepts / API

### Routing

Each plugin can export routable extensions, which are then imported into the app and mounted at a path.

First you will need a `RouteRef` instance to serve as the mount point of your
extensions. This can be used within your own plugin to create a link to the
extension page using `useRouteRef`, as well as for other plugins to link to your
extension.

It is best to place these in a separate top-level `src/routes.ts` file, in order
to avoid import cycles, for example like this:

```
/* src/routes.ts */
import { createRouteRef } from '@backstage/core-plugin-api';
// Note: This route ref is for internal use only, don't export it from the plugin
export const rootRouteRef = createRouteRef({
  id: 'Example Page',
});
```
Now that we have a `RouteRef`, we import it into `src/plugin.ts`, create our
plugin instance with `createPlugin`, as well as create and wrap our routable
extension using `createRoutableExtension` from `@backstage/core-plugin-api`:

```
/* src/plugin.ts */
import { createPlugin, createRouteRef } from '@backstage/core-plugin-api';
import ExampleComponent from './components/ExampleComponent';
// Create a plugin instance and export this from your plugin package
export const examplePlugin = createPlugin({
  id: 'example',
  routes: {
    root: rootRouteRef, // This is where the route ref should be exported for usage in the app
  },
});
// This creates a routable extension, which are typically full pages of content.
// Each extension should also be exported from your plugin package.
export const ExamplePage = examplePlugin.provide(
  createRoutableExtension({
    name: 'ExamplePage',
    // The component needs to be lazy-loaded. It's what will actually be rendered in the end.
    component: () =>
      import('./components/ExampleComponent').then(m => m.ExampleComponent),
    // This binds the extension to this route ref, which allows for routing within and across plugin extensions
    mountPoint: rootRouteRef,
  }),
);
```
This extension can then be imported and used in the app as follow, typically
placed within the top-level `<FlatRoutes>`:

```
<Route path="/any-path" element={<ExamplePage />} />
```

# Citations

1. Source page: https://backstage.io/docs/plugins/plugin-development
