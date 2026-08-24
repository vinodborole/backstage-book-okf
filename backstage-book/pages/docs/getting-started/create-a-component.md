---
type: Web Page
title: Create a Component | Backstage Software Catalog and Developer Platform
description: Leverage the scaffolder to start creating components with best practices.
resource: https://backstage.io/docs/getting-started/create-a-component
timestamp: '2026-08-24T06:57:24.152587+00:00'
---

# Create a Component

Audience: Developers

## Overview

Components can be created in the Software Catalog using software templates. Templates load skeletons of code, which can include some variables, and incorporate your company's best practices. The templates are published to a location, such as GitHub or GitLab.

The standalone Backstage application includes the `Example Node.js Template`, which is an example template for the scaffolder that creates and registers a simple Node.js service. You can also [create your own templates](/docs/features/software-templates/adding-templates).

## Prerequisites

For this example, the default Node.js template will be used. The template creates a repository in GitHub and adds the necessary files to it so that the component is integrated into the Software Catalog. Because you are creating a repository, you must first create an integration between Backstage and GitHub.

- 
You should have already [installed a standalone app](/docs/getting-started/) .
- 
Register the [GitHub Scaffolder Action module](/docs/features/software-templates/builtin-actions#installing-action-modules) .
- 
[Set up a GitHub Integration](/docs/getting-started/config/authentication#setting-up-a-github-integration) with Backstage, using a GitHub Personal Access Token.

## Creating the component

To create the component:

1. 
Select `Create` .
2. 
Select `Service` in the`CATEGORIES` dropdown list.
3. 
Select the `Owner` . For this example, you can select`guest` .
4. 
Select `Choose` in the`Example Node.js Template` .
5. 
For this example, enter `tutorial` for the`Name` of the service and select`NEXT` .
6. 
Enter your GitHub user name as the `Owner` .
7. 
Enter `tutorial` for the`Repository` and select`REVIEW` .
8. 
Review the information and select `CREATE` .

You can follow along with the progress, and as soon as every step is finished, you can take a look at your new service in either the repository or the Catalog.

Selecting `REPOSITORY` displays the `catalog-info.yaml`file and other project setup files that were created for the new component in the main branch of the `tutorial` repository.

The `catalog-info.yaml` file describes the entity for the Software Catalog. [Descriptor Format of Catalog Entities](/docs/features/software-catalog/descriptor-format) provides additional information.

```
apiVersion: backstage.io/v1alpha1
kind: Component
metadata:
  name: 'tutorial'
spec:
  type: service
  owner: user:guest
  lifecycle: experimental
```
Selecting `OPEN IN CATALOG` displays details of the new component, such as its relationships, links, and subcomponents.

Selecting `Home` in the sidebar, displays the new `tutorial` component in the Catalog.

# Citations

1. Source page: https://backstage.io/docs/getting-started/create-a-component
