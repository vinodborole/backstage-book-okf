---
type: Web Page
title: Backstage Project Structure | Backstage Software Catalog and Developer Platform
description: Introduction to files and folders in the Backstage Project repository
resource: https://backstage.io/docs/contribute/project-structure
timestamp: '2026-07-06T13:23:17.605783+00:00'
---

# Backstage Project Structure

Backstage is a complex project, and the GitHub repository contains many different files and folders. This document aims to clarify the purpose of those files and folders.

## General purpose files and folders

In the project root, there are a set of files and folders which are not part of the project as such, and may or may not be familiar to someone looking through the code.

- 
`.changeset/`- This folder contains files outlining which changes occurred in the project since the last release. These files are added manually, but managed by changesets and will be removed at every new release. They are essentially building-blocks of a CHANGELOG.
- 
`.github/`- Standard GitHub folder. It contains - amongst other things - our workflow definitions and templates. Worth noting is the vale sub-folder which is used for a markdown spellchecker.
- 
`.yarn/`- Backstage ships with its own`yarn`implementation. This allows us to have better control over our`yarn.lock`file and hopefully avoid problems due to yarn versioning differences.
- 
`contrib/`- Collection of examples or resources contributed by the community. We really appreciate contributions in here and encourage them being kept up to date.
- 
`docs/`- This is where we keep all of our documentation Markdown files. These end up on https://backstage.io/docs. Just keep in mind that changes to the`sidebars.ts`file may be needed as sections are added/removed.
- 
`.editorconfig`- A configuration file used by most common code editors. Learn more at EditorConfig.org.
- 
`.imgbotconfig`- Configuration for a bot which helps reduce image sizes.

## Monorepo packages

Every folder in both `packages/` and `plugins/` is within our monorepo setup, as
defined in
`package.json`:

```
  "workspaces": [
    "packages/*",
    "plugins/*"
  ],
```
Let's look at them individually.

`packages/`

These are all the packages that we use within the project. Plugins are separated out into their own folder, see further down.

- 
`app/`- This is our take on how an App could look like, bringing together a set of packages and plugins into a working Backstage App. This is not a published package, and the main goals are to provide a demo of what an App could look like and to enable local development.
- 
`backend/`- Every standalone Backstage project will have both an`app`*and*a`backend`package. The`backend`uses plugins to construct a working backend that the frontend (`app`) can use.
- 
`backend-app-api/`- This package contains the central wiring for how to make Backstage backends.
- 
`backend-plugin-api/`- This package contains the core APIs that are used to make Backstage backend features such as plugins and modules.
- 
`catalog-client`- An isomorphic client to interact with the Software Catalog. Backend plugins can use the package directly. Frontend plugins can use the client by using`@backstage/plugin-catalog`in combination with`useApi`and the`catalogApiRef`.
- 
`catalog-model/`- You can consider this to be a library for working with the catalog of sorts. It contains the definition of an Entity, as well as validation and other logic related to it. This package can be used in both the frontend and the backend.
- 
`cli/`- One of the biggest packages in our project, the`cli`is used to build, serve, diff, create plugins and more. In the early days of this project, we started out with calling tools directly - such as`eslint`- through`package.json`. But as it was tricky to have a good development experience around that when we change named tooling, we opted for wrapping those in our own CLI. That way everything looks the same in`package.json`. Much like react-scripts.
- 
`cli-common/`- This package mainly handles path resolving. It is a separate package to reduce bugs in CLI. We also want as few dependencies as possible to reduce download time when running the CLI which is another reason this is a separate package.
- 
`config/`- The way we read configuration data. This package can take a bunch of config objects and merge them together. app-config.yaml is an example of an config object.
- 
`config-loader/`- This package is used to read config objects. It does not know how to merge, but only reads files and passes them on to the config. As this part is only used by the backend, we chose to separate`config`and`config-loader`into two different packages.
- 
`core-app-api/`- This package contains the core APIs that are used to wire together Backstage apps.
- 
`core-components/`- This package contains our visual React components, some of which you can find in plugin examples.
- 
`core-plugin-api/`- This package contains the core APIs that are used to build Backstage plugins.
- 
`create-app/`- An CLI to specifically scaffold a new Backstage App. It does so by using a template.
- 
`dev-utils/`- Helps you setup a plugin for isolated development so that it can be served separately. This is for plugins using the legacy frontend system.
- 
`frontend-dev-utils/`- Utilities for developing frontend plugins using the new frontend system. Provides the`createDevApp`helper for setting up a minimal development app in a plugin's`dev/`entry point.
- 
`e2e-test/`- Another CLI that can be run to try out what would happen if you build all the packages, publish them, create a new app, and then run them. CI uses this for e2e-tests.
- 
`integration/`- Common functionalities of integrations like GitHub, GitLab, etc.
- 
`.storybook/`- This folder contains the Storybook configuration which helps visualize our reusable React components. Stories are scanned from packages and plugins across the monorepo, and are published in the Backstage Storybook.
- 
`techdocs-node/`- Common node.js functionalities for TechDocs, to be shared between techdocs-backend plugin and techdocs-cli.
- 
`test-utils/`- This package contains general purpose testing facilities for testing a Backstage App or its plugins.
- 
`theme/`- Holds the Backstage Theme.

`plugins/`

Most of the functionality of a Backstage App comes from plugins. Even core features can be plugins, take the catalog as an example.

We can categorize plugins into three different types; **Frontend**, **Backend**
and **GraphQL**. We differentiate these types of plugins when we name them, with
a dash-suffix. `-backend` means it’s a backend plugin and so on.

One reason for splitting a plugin is because of its dependencies. Another reason is for clear separation of concerns.

Take a look at our Plugin Directory or browse
through the
`plugins/` folder.

## Packages outside of the monorepo

For convenience we include packages in our project that are not part of our monorepo setup.

- `microsite/`- This folder contains the source code for backstage.io. It is built with Docusaurus. This folder is not part of the monorepo due to dependency reasons. Look at the microsite README for instructions on how to run it locally.

## Root files specifically used by the `app`

These files are kept in the root of the project mostly by historical reasons. Some of these files may be subject to be moved out of the root sometime in the future.

- 
`.npmrc`- It's common for companies to have their own npm registry, and this file makes sure that this folder always uses the public registry.
- 
`.yarnrc.yml`- Enforces "our" version of Yarn.
- 
`app-config.yaml`- Configuration for the app, both frontend and backend.
- 
`catalog-info.yaml`- Description of Backstage in the Backstage Entity format.

# Citations

1. Source page: https://backstage.io/docs/contribute/project-structure
