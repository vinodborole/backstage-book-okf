---
type: Web Page
title: TechDocs Documentation | Backstage Software Catalog and Developer Platform
description: TechDocs is Spotify’s homegrown docs-like-code solution built directly
  into Backstage
resource: https://backstage.io/docs/features/techdocs
timestamp: '2026-07-06T13:23:17.605783+00:00'
---

# TechDocs Documentation

## What is it?

TechDocs is Spotify’s homegrown docs-like-code solution built directly into Backstage. Engineers write their documentation in Markdown files which live together with their code - and with little configuration get a nice-looking doc site in Backstage.

Today, it is one of the core products in Spotify’s developer experience offering with 5000+ documentation sites and around 10000 average daily hits. Read more about TechDocs in its announcement blog post. 🎉

## Features

- Deploy TechDocs no matter how your software environment is set up.
- Discover your Service's technical documentation from the Service's page in Backstage Catalog.
- Create documentation-only sites for any purpose by just writing Markdown.
- Take advantage of the TechDocs Addon Framework to add features on top of the base docs-like-code experience.
- Explore and take advantage of the large ecosystem of MkDocs plugins to create a rich reading experience.
- Search for and find docs.

## Project roadmap

### Now

No current plans.

### Next

No current plans.

### Someday/Maybe

- What can we do in TechDocs to help drive up documentation quality? We have many ideas, for example, a Trust Card with associated Trust Score and automatic triggering of documentation maintenance notifications.
- Contribute to and deploy from a marketplace of TechDocs Addons
- Addon: MDX (allows you to use JSX in your Markdown content)
- Can we go static site generator agnostic?
- Better integration with Scaffolder V2 (e.g. easy to choose and apply documentation template with Software Templates)
- Possible to configure several aspects about TechDocs (e.g. URL, homepage, theme)

### Done

See Done below for a list of completed roadmap items.

## Supported

The following sections show the source code hosting providers and file storage providers that are currently supported by TechDocs.

See TechDocs Architecture to get an overview of where the below providers are used.

### Source code hosting providers

| Source Code Hosting Provider | Support Status | 
|---|---|
| GitHub | Yes ✅ | 
| GitHub Enterprise | Yes ✅ | 
| Bitbucket | Yes ✅ | 
| Azure DevOps | Yes ✅ | 
| Gerrit | Yes ✅ | 
| GitLab | Yes ✅ | 
| GitLab Enterprise | Yes ✅ | 
| Gitea | Yes ✅ | 
| AWS CodeCommit | Yes ✅ | 
| Harness Code | Yes ✅ | 

### File storage providers

| File Storage Provider | Support Status | 
|---|---|
| Local Filesystem of Backstage app | Yes ✅ | 
| Google Cloud Storage (GCS) | Yes ✅ | 
| Amazon Web Services (AWS) S3 | Yes ✅ | 
| Azure Blob Storage | Yes ✅ | 
| OpenStack Swift | Community ✅ | 

Reach out to us if you want to request more providers.

## Tech stack

| Stack | Location | 
|---|---|
| Frontend Plugin | @backstage/plugin-techdocs | 
| Frontend Plugin Library | @backstage/plugin-techdocs-react | 
| Backend Plugin | @backstage/plugin-techdocs-backend | 
| CLI (for local development and generating docs) | @techdocs/cli | 
| Docker Container (for generating docs) | techdocs-container | 

## Get involved

Reach out to us in the **#techdocs** channel of our
Discord chatroom.

## Done

**Alpha release**

- Alpha of TechDocs that you can use end to end - and contribute to.

**Beta release**

- TechDocs' recommended setup supports most environments (CI systems, cloud storage solutions, source control systems).
- Instructions for upgrading from Alpha to Beta

**v1.0**

TechDocs promoted to v1.0! To understand how this change affects the package, check out our versioning policy.

TechDocs packages:

- @backstage/plugin-techdocs
- @backstage/plugin-techdocs-backend
- @backstage/plugin-techdocs-node
- @techdocs/cli

**TechDocs Addon Framework**

With the Backstage 1.2 release, we introduced the TechDocs Addon Framework for augmenting the TechDocs experience at read-time.

In addition to the framework itself, we open sourced a **ReportIssue** Addon, helping you to create a feedback loop that drives up documentation quality and foster a documentation culture at your organization.

# Citations

1. Source page: https://backstage.io/docs/features/techdocs
