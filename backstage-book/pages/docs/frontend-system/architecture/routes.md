---
type: Web Page
title: Frontend Routes | Backstage Software Catalog and Developer Platform
description: Frontend routes
resource: https://backstage.io/docs/frontend-system/architecture/routes
timestamp: '2026-07-06T13:23:17.605783+00:00'
---

# Frontend Routes

## Introduction

Each Backstage plugin is an isolated piece of functionality that doesn't typically communicate directly with other plugins. In order to achieve this, there are many parts of the frontend system that provide a layer of indirection for cross-plugin communication, and the routing system is one of them.

The Backstage routing system makes it possible to implement navigation across plugin boundaries, without each individual plugin knowing the concrete path or location of other plugins in the routing hierarchy, or even its own. This is achieved through the concept of route references, which are opaque reference values that can be shared and used to create concrete links to different parts of an app. The route ref paths can be configured both at plugin level (by plugin developers) and at the app level (by integrators). It is up to plugin developers to create route references for any page content in their plugin that they want it to be possible to link to or from.

## Route References

Plugin developers create a `RouteRef` to expose a path in Backstage's routing system. You will see below how routes are defined programmatically, but before diving into code, let us explain how to configure them at the app level. In spite of the fact that plugin developers choose a default route path for the routes their plugin provides, paths are configurable, so app integrators can set a custom path to a route whenever they like to (more information in the following sections).

There are three types of route references: regular route, sub route, and external route, and we will cover both the concept and code definition for each.

### Creating a Route Reference

Route references, also known as "absolute" or "regular" routes, are created as follows:

```
import { createRouteRef } from '@backstage/frontend-plugin-api';
// Creates a route reference, which is not yet associated with any plugin page
export const indexRouteRef = createRouteRef();
```
Note that you often want to create the route references themselves in a different file than the one that creates the plugin instance, for example a top-level `routes.ts`. This is to avoid circular imports when you use the route references from other parts of the same plugin.

Route refs do not have any behavior themselves. They are an opaque value that represents route targets in an app, which are bound to specific paths at runtime. Their role is to provide a level of indirection to help link together different pages that otherwise wouldn't know how to route to each other.

### Providing Route References to Plugins

The code snippet in the previous section does not indicate which plugin the route belongs to. To do so, you have to use it in the creation of any kind of routable extension, such as a page extension:

```
import {
  createFrontendPlugin,
  createPageExtension,
} from '@backstage/frontend-plugin-api';
import { indexRouteRef } from './routes';
const catalogIndexPage = createPageExtension({
  // The `name` option is omitted because this is an index page
  path: '/entities',
  routeRef: indexRouteRef,
  loader: () => import('./components').then(m => <m.IndexPage />),
});
export default createFrontendPlugin({
  pluginId: 'catalog',
  routes: {
    index: indexRouteRef,
  },
  extensions: [catalogIndexPage],
});
```
In the example above we associated the `indexRouteRef` with the `catalogIndexPage` extension and provided both the route ref and page via the Catalog plugin. So, when this plugin is installed in the app, the index page will become associated with the newly created `RouteRef`, making it possible to use the route ref to navigate the page extension.

It may seem unclear why we configure the `routes` option when creating a plugin as the route has already been passed to the extension. We do that to make it possible for other plugins to route to our page, which is explained in detail in the binding routes section.

### Defining References with Path Parameters

Route references optionally accept a `params` option, which will require the listed parameter names to be present in the route path. Here is how you create a reference for a route that requires a `kind`, `namespace` and `name` parameters, like in this path `/entities/:kind/:namespace/:name`:

```
import { createRouteRef } from '@backstage/frontend-plugin-api';
export const detailsRouteRef = createRouteRef({
  // The parameters that must be included in the path of this route reference
  params: ['kind', 'namespace', 'name'],
});
```
### Using a Route Reference

Route references can be used to link to page in the same plugin, or to pages in different plugins. In this section we will cover the first scenario. If you are interested in linking to a page of a different plugin, please go to the external routes section below.

Suppose we are creating a plugin that renders a Catalog index page with a link to a "Foo" component details page. Here is the code for the index page:

```
import { useRouteRef } from '@backstage/frontend-plugin-api';
import { detailsRouteRef } from '../routes';
export const IndexPage = () => {
  const getDetailsPath = useRouteRef(detailsRouteRef);
  return (
    <div>
      <h1>Index Page</h1>
      {getDetailsPath && (
        <a
          href={getDetailsPath({
            kind: 'component',
            namespace: 'default',
            name: 'foo',
          })}
        >
          See "Foo" details
        </a>
      )}
    </div>
  );
};
```
We use the `useRouteRef` hook to create a link generator function that returns the details page path. First we need to check whether the route is available, the link generator function will be `undefined` if it isn't. We then call the link generator, passing it an object with the kind, namespace, and name. These parameters are used to construct a concrete path to the "Foo" details page.

Let's see how the details page can get the parameters from the URL:

```
import { useRouteRefParams } from '@backstage/frontend-plugin-api';
import { detailsRouteRef } from '../routes';
export const DetailsPage = () => {
  const params = useRouteRefParams(detailsRouteRef);
  return (
    <div>
      <h1>Details Page</h1>
      <ul>
        <li>Kind: {params.kind}</li>
        <li>Namespace: {params.namespace}</li>
        <li>Name: {params.name}</li>
      </ul>
    </div>
  );
};
```
In the code above, we are using the `useRouteRefParams` hook to retrieve the entity-composed id from the URL. The parameter object contains three values: kind, namespace, and name. We can display these values or call an API using them.

Since we are linking to pages of the same package, we are using a route ref directly. However, in the following sections, you will see how to link to pages of different plugins.

## External Route References

External routes are made for linking to a page of an external plugin. For this section example, let's assume that we want to link from the Catalog entities list page to the Scaffolder create component page.

We don't want to reference the Scaffolder plugin directly, since that would create an unnecessary dependency. It would also provide little flexibility in allowing the app to tie plugins together, with the links instead being dictated by the plugins themselves. To solve this, we use an `ExternalRouteRef`. Much like regular route references, they can be passed to `useRouteRef` to create concrete URLs, but they can not be used in page extensions and instead have to be associated with a target route using route bindings in the app.

We create a new `RouteRef` inside the Scaffolder plugin, using a neutral name that describes its role in the plugin rather than a specific plugin page that it might be linking to, allowing the app to decide the final target. If the Catalog entity list page for example wants to link the Scaffolder create component page in the header, it might declare an `ExternalRouteRef` similar to this:

```
import { createExternalRouteRef } from '@backstage/frontend-plugin-api';
export const createComponentExternalRouteRef = createExternalRouteRef();
```
External routes are also used in a similar way as regular routes:

```
import { useRouteRef } from '@backstage/frontend-plugin-api';
import { createComponentExternalRouteRef } from '../routes';
export const IndexPage = () => {
  const getCreateComponentPath = useRouteRef(createComponentExternalRouteRef);
  return (
    <div>
      <h1>Index Page</h1>
      {getCreateComponentPath && (
        <a href={getCreateComponentPath()}>Create Component</a>
      )}
    </div>
  );
};
```
Given the above binding, using `useRouteRef(createComponentExternalRouteRef)` within the Catalog plugin will let us create a link to whatever path the Scaffolder create component page is mounted at. Note that there is no direct dependency between the Catalog plugin and Scaffolder, that is, we are not importing the `createComponentExternalRouteRef` from the Scaffolder package.

Now the only thing left is to provide the page and external route via a plugin:

```
import {
  createFrontendPlugin,
  createPageExtension,
  useRouteRef,
} from '@backstage/frontend-plugin-api';
import { indexRouteRef, createComponentExternalRouteRef } from './routes';
const catalogIndexPage = createPageExtension({
  path: '/entities',
  routeRef: indexRouteRef,
  loader: () => import('./components').then(m => <m.IndexPage />),
});
export default createFrontendPlugin({
  pluginId: 'catalog',
  routes: {
    index: indexRouteRef,
  },
  externalRoutes: {
    createComponent: createComponentExternalRouteRef,
  },
  extensions: [catalogIndexPage],
});
```
External routes can also have parameters. For example, if you want to link to an entity's details page from Scaffolder, you'll need to create an external route that receives the same parameters the Catalog details page expects:

```
import { createExternalRouteRef } from '@backstage/frontend-plugin-api';
export const entityDetailsExternalRouteRef = createExternalRouteRef({
  params: ['kind', 'namespace', 'name'],
});
```
Now let's move on and configure the app to resolve these external routes, so that the Scaffolder links to the Catalog entity page, and the Catalog links to the Scaffolder page.

### Binding External Route References

The association of external routes is controlled by the app. Each `ExternalRouteRef` of a plugin should be bound to an actual `RouteRef`, usually from another plugin. The binding process happens once at app startup, and is then used through the lifetime of the app to help resolve concrete route paths.

Using the above example of the Catalog entities list page to the Scaffolder create component page, we might do something like this in the app configuration file:

```
app:
  routes:
    bindings:
      # point to the Scaffolder create component page when the Catalog create component ref is used
      catalog.createComponent: scaffolder.index
      # point to the Catalog details page when the Scaffolder component details ref is used
      scaffolder.componentDetails: catalog.details
      # explicitly disable the default route binding from the scaffolder to the catalog import page
      scaffolder.registerComponent: false
```
We also have the ability to express this in code as an option to `createApp`, but you of course only need to use one of these two methods:

```
import { createApp } from '@backstage/frontend-defaults';
import catalog from '@backstage/plugin-catalog';
import scaffolder from '@backstage/plugin-scaffolder';
const app = createApp({
  bindRoutes({ bind }) {
    bind(catalog.externalRoutes, {
      createComponent: scaffolder.routes.createComponent,
    });
    bind(scaffolder.externalRoutes, {
      componentDetails: catalog.routes.details,
      registerComponent: false,
    });
  },
});
export default app.createRoot();
```
Note that we are not importing and using the `RouteRef`s directly in the app, and instead rely on the plugin instance to access routes of the plugins. This provides better namespacing and discoverability of routes, as well as reduce the number of separate exports from each plugin package.

Another thing to note is that this indirection in the routing is particularly useful for open source plugins that need to provide flexibility in how they are integrated. For plugins that you build internally for your own Backstage application, you can choose to use direct imports or even concrete route path strings directly. Although there can be some benefits to using the full routing system even in internal plugins: it can help you structure your routes, and as you will see further down it also helps you manage route parameters.

### Default Targets for External Route References

It is possible to define a default target for an external route reference, potentially removing the need to bind the route in the app. This reduces the need for configuration when installing new plugins through providing a sensible default. It is of course still possible to override the route binding in the app, as long as the external route ref is exported via the `externalRoutes` property of the plugin instance.

The default target uses the same syntax as the route binding configuration, and will only be used if the target plugin and route exist. For example, this is how the catalog can define a default target for the create component external route in a way that removes the need for the binding in the previous example:

```
import { createExternalRouteRef } from '@backstage/frontend-plugin-api';
export const createComponentExternalRouteRef = createExternalRouteRef({
  defaultTarget: 'scaffolder.createComponent',
});
```
## Sub Route References

The last kind of route ref that can be created is a `SubRouteRef`, which can be used to create a route ref with a fixed path relative to an absolute `RouteRef`. They are useful if you have a page that internally is mounted at a sub route of a page extension component, and you want other plugins to be able to route to that page. And they can be a useful utility to handle routing within a plugin itself as well.

For example:

```
import {
  createRouteRef,
  createSubRouteRef,
} from '@backstage/frontend-plugin-api';
export const indexRouteRef = createRouteRef();
export const detailsSubRouteRef = createSubRouteRef({
  parent: indexRouteRef,
  path: '/details',
});
```
There are substantial differences between creating subroutes and regular or external routes because subroutes are associated with regular routes, and the sub route path must be specified. The path string must include the parameters if this sub route has them:

```
// Omitting rest of the previous example file
export const detailsSubRouteRef = createSubRouteRef({
  parent: indexRouteRef,
  path: '/:name/:namespace/:kind',
});
```
Using subroutes in a page extension is as simple as this:

```
import { Routes, Route, useLocation } from 'react-router-dom';
import { useRouteRef } from '@backstage/frontend-plugin-api';
import { indexRouteRef, detailsSubRouteRef } from '../routes';
import { DetailsPage } from './DetailsPage';
export const IndexPage = () => {
  const { pathname } = useLocation();
  const getIndexPath = useRouteRef(indexRouteRef);
  const getDetailsPath = useRouteRef(detailsSubRouteRef);
  return (
    <div>
      <h1>Index Page</h1>
      {/* Linking to the details sub route */}
      {pathname === getIndexPath?.() ? (
        <a
          {/* Setting the details sub route params */}
          href={getDetailsPath?.({
            kind: 'component',
            namespace: 'default',
            name: 'foo',
          })}
        >
          Show details
        </a>
      ) : (
        <a href={getIndexPath?.()}>Hide details</a>
      )}
      {/* Registering the details sub route */}
      <Routes>
        <Route path={detailsSubRouteRef.path} element={<DetailsPage />} />
      </Routes>
    </div>
  );
};
```
This is how you can get the parameters of a sub route URL:

```
import { useParams } from 'react-router-dom';
export const DetailsPage = () => {
  const params = useParams();
  return (
    <div>
      <h1>Details Sub Page</h1>
      <ul>
        <li>Kind: {params.kind}</li>
        <li>Namespace: {params.namespace}</li>
        <li>Name: {params.name}</li>
      </ul>
    </div>
  );
};
```
Finally, see how a plugin can provide subroutes:

```
import {
  createFrontendPlugin,
  createPageExtension,
} from '@backstage/frontend-plugin-api';
import { indexRouteRef, detailsSubRouteRef } from './routes';
const catalogIndexPage = createPageExtension({
  path: '/entities',
  routeRef: indexRouteRef,
  loader: () => import('./components').then(m => <m.IndexPage />),
});
export default createFrontendPlugin({
  pluginId: 'catalog',
  routes: {
    index: indexRouteRef,
    details: detailsSubRouteRef,
  },
  extensions: [catalogIndexPage],
});
```
## Route Aliases - Overriding Routed Extensions in Modules

It is possible to override extensions of a plugin using a module. In some cases the extension you're overriding may require a route reference. You could import the plugin instance and access the it via the `routes` property, but this creates a direct dependency on the plugin and risks leading to package duplication issues that would also break the route reference.

Instead of accessing the route reference directly, you can create a new route reference that acts as an alias for the original one from the plugin. For example, you can override the catalog index page with a custom one like this:

```
const indexRouteRef = createRouteRef({ aliasFor: 'catalog.catalogIndex' });
export default createFrontendModule({
  pluginId: 'catalog',
  extensions: [
    PageBlueprint.make({
      params: {
        defaultPath: '/catalog',
        routeRef: indexRouteRef,
        loader: () =>
          import('./CustomCatalogIndexPage').then(m => (
            <m.CustomCatalogIndexPage />
          )),
      },
    }),
  ],
});
```
Aliases are limited to the plugin that they are defined in. These aliases can also be imported and used as usual with for example `useRouteRef`, but they must always be registered in the app via an extension for this to work. For example, the following will not work:

```
function MyInvalidComponent() {
  // This is NOT valid
  const link = useRouteRef(
    createRouteRef({ aliasFor: 'catalog.catalogIndex' }),
  );
  // ...
}
```

# Citations

1. Source page: https://backstage.io/docs/frontend-system/architecture/routes
