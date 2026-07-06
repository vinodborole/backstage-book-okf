---
type: Web Page
title: TechDocs FAQ | Backstage Software Catalog and Developer Platform
description: This page answers frequently asked questions about TechDocs
resource: https://backstage.io/docs/features/techdocs/faqs
timestamp: '2026-07-06T13:23:17.605783+00:00'
---

# TechDocs FAQ

This page answers frequently asked questions about TechDocs.

## Technology

- What static site generator is TechDocs using?
- What is the mkdocs-techdocs-core plugin?
- Does TechDocs support file formats other than Markdown (e.g. RST, AsciiDoc)?
- What should be the value of `backstage.io/techdocs-ref`when using external build and storage?
- Is it possible for users to suggest changes or provide feedback on a TechDocs page?

#### What static site generator is TechDocs using?

TechDocs is using MkDocs to build project documentation under the hood. Documentation built with the techdocs-container is using the MkDocs Material Theme.

#### What is the mkdocs-techdocs-core plugin?

The mkdocs-techdocs-core package is a MkDocs Plugin that works like a wrapper around multiple MkDocs plugins (e.g. MkDocs Monorepo Plugin) as well as a selection of Python Markdown extensions that TechDocs supports.

#### Does TechDocs support file formats other than Markdown (e.g. RST, AsciiDoc)?

Not right now. We are currently using MkDocs to generate the documentation from source, so the files have to be in Markdown format. However, in the future we want to support other static site generators which will make it possible to use other file formats.

#### What should be the value of `backstage.io/techdocs-ref` when using external build and storage?

The value of
`backstage.io/techdocs-ref`
metadata annotation is used in the build process of TechDocs. But when
`techdocs.builder` is set to `'external'` in
`app-config.yaml`, the value of the annotation remains unused. However the
annotation should still be present in entity descriptor file (e.g.
`catalog-info.yaml`) for Backstage to know that TechDocs is enabled for the
entity.

#### What happens when you navigate to a TechDocs URL for an entity uses the `backstage.io/techdocs-entity` annotation?

If you navigate to a TechDocs URL in the format `docs/{namespace}/{kind}/{name}` for an entity that has the `backstage.io/techdocs-entity` annotation (instead of the `backstage.io/techdocs-ref` annotation), then Backstage will redirect to the TechDocs page of the entity referenced in the value of that annotation.

#### Is it possible for users to suggest changes or provide feedback on a TechDocs page?

This is supported for TechDocs sites whose source code is hosted in either
GitHub or GitLab. In order to add "edit this page" and "leave feedback" buttons
on a TechDocs page, be sure that you have `repo_url` and `edit_uri` values in
your `mkdocs.yml` files per
MkDocs instructions.

If the host name of your source code hosting URL does not include `github` or
`gitlab`, an `integrations` entry in your `app-config.yaml` pointed at your
source code provider is also needed (only the `host` key is necessary).

# Citations

1. Source page: https://backstage.io/docs/features/techdocs/faqs
