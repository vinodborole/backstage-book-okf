---
type: Web Page
title: Backstage Project Structure | Backstage Software Catalog and Developer Platform
description: Introduction to files and folders in the Backstage Project repository
resource: https://backstage.io/docs/contribute/project-structure
timestamp: '2026-07-09T12:16:50.465553+00:00'
---

# Backstage Project Structure

Backstage is a complex project, and the GitHub repository contains many different files and folders. This document aims to clarify the purpose of those files and folders.

## General purpose files and folders

In the project root, there are a set of files and folders which are not part of the project as such, and may or may not be familiar to someone looking through the code.

- 
`.changeset/`[changesets](https://github.com/atlassian/changesets)and will be removed at every new release. They are essentially building-blocks of a CHANGELOG.
- 
`.github/`[vale](https://github.com/backstage/backstage/tree/master/.github/vale)sub-folder which is used for a markdown spellchecker.
- 
`.yarn/``yarn`implementation. This allows us to have better control over our`yarn.lock`file and hopefully avoid problems due to yarn versioning differences.
- 
`contrib/`
- 
`docs/`[https://backstage.io/docs](https://backstage.io/docs). Just keep in mind that changes to the`sidebars.ts`
- 
`.editorconfig`[EditorConfig.org](https://editorconfig.org/).
- 
`.imgbotconfig`[bot](https://imgbot.net/)which helps reduce image sizes.

## Monorepo packages

Every folder in both `packages/` and `plugins/` is within our monorepo setup, as
defined in
[ package.json](https://github.com/backstage/backstage/blob/master/package.json):

```
  "workspaces": [
    "packages/*",
    "plugins/*"
  ],
```
Let's look at them individually.

`packages/`

These are all the packages that we use within the project. [Plugins](#plugins)
are separated out into their own folder, see further down.

- 
`app/`
- 
`backend/``app`*and*a`backend`package. The`backend`uses plugins to construct a working backend that the frontend (`app`) can use.
- 
`backend-app-api/`
- 
`backend-plugin-api/`
- 
`catalog-client``@backstage/plugin-catalog`in combination with`useApi`and the`catalogApiRef`.
- 
`catalog-model/`[Entity](https://backstage.io/docs/features/software-catalog/references#docsNav), as well as validation and other logic related to it. This package can be used in both the frontend and the backend.
- 
`cli/``cli`is used to build, serve, diff, create plugins and more. In the early days of this project, we started out with calling tools directly - such as`eslint`- through`package.json`. But as it was tricky to have a good development experience around that when we change named tooling, we opted for wrapping those in our own CLI. That way everything looks the same in`package.json`. Much like[react-scripts](https://github.com/facebook/create-react-app/tree/master/packages/react-scripts).
- 
`cli-common/`[CLI](https://github.com/backstage/backstage/tree/master/packages/cli). We also want as few dependencies as possible to reduce download time when running the CLI which is another reason this is a separate package.
- 
`config/`[app-config.yaml](https://github.com/backstage/backstage/blob/master/app-config.yaml)is an example of an config object.
- 
`config-loader/``config`and`config-loader`into two different packages.
- 
`core-app-api/`
- 
`core-components/`[plugin examples](https://backstage.io/storybook/?path=/story/plugins-examples--plugin-with-data).
- 
`core-plugin-api/`
- 
`create-app/`[template](https://github.com/backstage/backstage/tree/master/packages/create-app/templates/default-app).
- 
`dev-utils/`
- 
`frontend-dev-utils/``createDevApp`helper for setting up a minimal development app in a plugin's`dev/`entry point.
- 
`e2e-test/`
- 
`integration/`
- 
`.storybook/`[Backstage Storybook](https://backstage.io/storybook).
- 
`techdocs-node/`[techdocs-backend](https://github.com/backstage/backstage/tree/master/plugins/techdocs-backend)plugin and[techdocs-cli](https://github.com/backstage/backstage/tree/master/packages/techdocs-cli).
- 
`test-utils/`
- 
`theme/`

`plugins/`

Most of the functionality of a Backstage App comes from plugins. Even core
features can be plugins, take the
[catalog](https://github.com/backstage/backstage/tree/master/plugins/catalog) as
an example.

We can categorize plugins into three different types; **Frontend**, **Backend**
and **GraphQL**. We differentiate these types of plugins when we name them, with
a dash-suffix. `-backend` means it’s a backend plugin and so on.

One reason for splitting a plugin is because of its dependencies. Another reason is for clear separation of concerns.

Take a look at our [Plugin Directory](https://backstage.io/plugins) or browse
through the
[ plugins/](https://github.com/backstage/backstage/tree/master/plugins) folder.

## Packages outside of the monorepo

For convenience we include packages in our project that are not part of our monorepo setup.

- `microsite/`- [Docusaurus](https://docusaurus.io/). This folder is not part of the monorepo due to dependency reasons. Look at the- [microsite README](https://github.com/backstage/backstage/blob/master/microsite/README.md)for instructions on how to run it locally.

## Root files specifically used by the `app`

These files are kept in the root of the project mostly by historical reasons. Some of these files may be subject to be moved out of the root sometime in the future.

- 
`.npmrc`
- 
`.yarnrc.yml`
- 
`app-config.yaml`
- 
`catalog-info.yaml`

# Citations

1. Source page: https://backstage.io/docs/contribute/project-structure
