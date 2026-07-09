---
type: Web Page
title: Backend Plugins | Backstage Software Catalog and Developer Platform
description: Backend plugins
resource: https://backstage.io/docs/backend-system/architecture/plugins
timestamp: '2026-07-09T12:16:50.465553+00:00'
---

# Backend Plugins

Plugins provide the actual base features of a Backstage backend. Each plugin operates completely independently of all other plugins and they only communicate with each other through network calls. This means that there is a strong degree of isolation between plugins, and that each plugin can be considered a separate microservice. While a default Backstage project has all plugins installed within a single backend, it is also possible to split this setup into multiple backends, with each backend housing one or more plugins.

## Defining a Plugin

Plugins are created using the `createBackendPlugin` function, and should typically be exported from a plugin package. All plugins must have an ID and a `register` method, where the ID matches the plugin ID in the package name, without the `-backend` suffix. See also the [dedicated section](/docs/backend-system/architecture/naming-patterns) about proper naming patterns.

```
// plugins/example-backend/src/plugin.ts
import {
  coreServices,
  createBackendPlugin,
} from '@backstage/backend-plugin-api';
export const examplePlugin = createBackendPlugin({
  pluginId: 'example',
  register(env) {
    env.registerInit({
      deps: {
        logger: coreServices.logger,
      },
      async init({ logger }) {
        logger.info('Hello from example plugin');
      },
    });
  },
});
```
The `env` object passed to the `register` callback contains different methods that declare the external surface of the plugin. The `env.registerInit` method is used to register an initialization function that is run when the backend starts up. The `deps` argument is used to declare service dependencies, and the `init` callback is passed an object with the resolved dependencies. In this case, we declare a dependency on the logger service, which is one of the core services available to all Backstage backend plugins. For a full list of core services as well as documentation for each services, see the [core services section](/docs/backend-system/core-services/index). Plugins can of course also depend on services exported by other libraries.

The `createBackendPlugin` return value is exported as `examplePlugin`, which is a factory function used to create the actual plugin instance. For example, to install the plugin in your backend instance, you would do the following:

```
import { examplePlugin } from 'backstage-plugin-example-backend';
backend.add(examplePlugin);
```
By convention every plugin package should export its plugin instance as the default export from the package:

```
// plugins/example-backend/src/index.ts
export { examplePlugin as default } from './plugin.ts';
```
This allows you to install the plugin in your backend instance by just referencing the package:

```
backend.add(import('backstage-plugin-example-backend'));
```
To make your plugins customizable you should generally prefer to use [static configuration](/docs/conf/defining). By convention plugins should place their configuration under a top-level configuration key that matches the plugin ID. For example, our example plugin might be configured as follows:

```
example:
  message: Welcome to the example plugin
```
For situations where static configuration is too limiting, you can instead register extension points for your plugin. Extension Points are covered in the [next section](/docs/backend-system/architecture/extension-points).

## Rules of Plugins

The following rules apply to the production setup of Backstage plugins in the broader Backstage plugin ecosystem. Any plugin that is maintained under the `@backstage` package namespace should follow these rules, and it is recommended that all widely distributed plugins follow these rules as well.

An exception to these rules are made for development or test setups, where shortcuts can be taken in order to streamline development and keep things simple.

### Scalable

Plugins must always be designed to be horizontally scalable. This means that you should not keep any state in memory, or make sure that replicating this state across multiple instances is not an issue. Plugins should either be stateless, or store their state in an external service, such as a database.

### Isolated

Plugins must never communicate with each other directly through code, they may only communicate over the network. Plugins that wish to expose an external interface for other plugins and modules to use are recommended to do so through a [node-library](/docs/tooling/cli/build-system#package-roles) package. The library should export an API client service to make calls to your plugin, or similar construct.

# Citations

1. Source page: https://backstage.io/docs/backend-system/architecture/plugins
