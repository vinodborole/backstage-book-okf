---
type: Web Page
title: Observability | Backstage Software Catalog and Developer Platform
description: Adding Observability to Your Plugin
resource: https://backstage.io/docs/plugins/observability
timestamp: '2026-07-06T13:23:17.605783+00:00'
---

# Observability

This section is part of the legacy plugins documentation. For new backend system logging, see the Logger and Root Logger core service documentation. For health checks, see Root Health.

This article briefly describes the observability options that are available to a Backstage integrator.

## Datadog RUM Events

See how to install Datadog Events in your app here.

## Logging

### New Backend

The backend supplies a central logging service,
`rootLogger`, as well as a plugin
based logger, `logger` from `coreServices`.
To add additional granularity to your logs, you can create children from the plugin
based logger, using the `.child()` method and provide it with JSON data. For example,
if you wanted to log items for a specific span in your plugin, you could do

```
export function createRouter({ logger }) {
  const router = Router();
  router.post('/task/:taskId/queue', (req, res) => {
    const { taskId } = req.params;
    const taskLogger = logger.child({ task: taskId });
    taskLogger.log('Queueing this task.');
  });
  router.get('/task/:taskId/results', (req, res) => {
    const { taskId } = req.params;
    const taskLogger = logger.child({ task: taskId });
    taskLogger.log('Getting the results of this task.');
  });
}
```
You can also add additional metadata to all logs for your Backstage instance by
overriding the `rootLogger` implementation, you can see an example in
the `rootLogger` docs.

### Old Backend

The backend supplies a central winston
root logger that plugins are expected to use for their logging needs. In the
default production setup, it emits structured JSON logs on stdout, with a field
`"service": "backstage"` and also tagged on a per-plugin basis. Plugins that
want to more finely specify what part of their processes that emitted the log
message should add a `"component"` field to do so.

An example log line could look as follows:

```
{
  "service": "backstage",
  "type": "plugin",
  "plugin": "catalog",
  "component": "catalog-all-locations-refresh",
  "level": "info",
  "message": "Locations Refresh: Refreshing location bootstrap:bootstrap"
}
```
## Health Checks

### New Backend (post 1.29.0)

The new backend provides a `RootHealthService` which implements
`/.backstage/health/v1/readiness` and `/.backstage/health/v1/liveness` endpoints
to provide health checks for the entire backend instance.

You can read more about this new service and how to customize it in the Root Health Service documentation.

### New Backend (pre 1.29.0)

The new backend is moving towards health checks being plugin-based, as such there is no current plugin for providing a health check route. You can add this yourself easily though,

```
import {
  coreServices,
  createBackendModule,
  createBackendPlugin,
} from '@backstage/backend-plugin-api';
const healthCheck = createBackendPlugin({
  pluginId: 'healthcheck',
  register(env) {
    env.registerInit({
      deps: {
        rootHttpRouter: coreServices.rootHttpRouter,
      },
      init: async ({ rootHttpRouter }) => {
        // You can adjust the route name and response as you need.
        rootHttpRouter.use('/healthcheck', (req, res) => {
          res.json({ status: 'ok' });
        });
      },
    });
  },
});
```
### Old Backend

The example old backend in the Backstage repository
supplies
a very basic health check endpoint on the `/healthcheck` route. You may add such
a handler to your backend as well, and supply your own logic to it that fits
your particular health checking needs.

# Citations

1. Source page: https://backstage.io/docs/plugins/observability
