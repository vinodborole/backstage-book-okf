---
type: Web Page
title: Create a Backstage Plugin | Backstage Software Catalog and Developer Platform
description: Documentation on How to Create a Backstage Plugin
resource: https://backstage.io/docs/plugins/create-a-plugin
timestamp: '2026-07-06T13:23:17.605783+00:00'
---

# Create a Backstage Plugin

This page describes creating plugins for the **old frontend system**. For creating plugins using the new frontend system, see Building Frontend Plugins. For creating backend plugins, see Building Backend Plugins and Modules.

A Backstage Plugin adds functionality to Backstage.

## Create a Plugin

To create a new frontend plugin, make sure you've run `yarn install` and installed
dependencies, then run the following on your command line (a shortcut to
invoking the
`backstage-cli new --select plugin`)
from the root of your project.

```
yarn new
```
And then select `frontend-plugin`.

This will create a new Backstage Plugin based on the ID that was provided. It will be built and added to the Backstage App automatically.

If the Backstage App is already running (with

`yarn start`) you should be able to see the default page for your new plugin directly by navigating to`http://localhost:3000/my-plugin`.

You can also serve the plugin in isolation by running `yarn start` in the plugin
directory. Or by using the yarn workspace command, for example:

```
yarn workspace @backstage/plugin-my-plugin start # Also supports --check
```
This method of serving the plugin provides quicker iteration speed and a faster
startup and hot reloads. It is only meant for local development, and the setup
for it can be found inside the plugin's `dev/` directory.

### Other Plugin Library Package Types

There are other plugin library package types that you can chose from. To be able to
select the type when you create a new plugin just run: `yarn new`. You'll then be asked
what type of plugin you wish to create like this:

# Citations

1. Source page: https://backstage.io/docs/plugins/create-a-plugin
