---
type: Web Page
title: Viewing entity relationships | Backstage Software Catalog and Developer Platform
description: View the relationships between the entities in the Catalog
resource: https://backstage.io/docs/getting-started/viewing-entity-relationships
timestamp: '2026-07-20T08:58:01.906190+00:00'
---

# Viewing entity relationships

Audience: All

Each of the entities in the Catalog has various relationships to each other. For example, the demo data includes an API that provides data to a website. `guests` is the owner of the API and the website, and anyone signed in as part of the `guests` group can maintain them.

To see these relationships:

- 
Select the name of the component in the main panel, in this example, `example-website`.A page is displayed that includes a `Relations`section. This section displays the selected entity and any other types of entities to which it is related. Each relationship is also designated, such as`hasPart/partOf`and`apiProvidedBy/providesApi`.[Well-known Relations between Catalog Entities](/docs/features/software-catalog/well-known-relations)describes the most common relationships, but you can also[create your own relationships](/docs/features/software-catalog/extending-the-model#adding-a-new-relation-type).
- 
Selecting any of the related entities allows you to drill down further through the system model. 

## Filtering the relationships

You can also view the relationships in the [Catalog Graph](/docs/features/software-catalog/creating-the-catalog-graph). This view allows you to filter what entities and relationships to display.

To display the Catalog Graph:

- 
Select the name of the component in the main panel, in this example, `example-website`.A page is displayed that includes a `Relations`section.
- 
Select `View graph`in the`Relations`section.The `Catalog Graph`is displayed.

### Setting the filters

The `Catalog Graph` automatically reflects any changes you make to the filter settings. You can set the following filters:

- 
`MAX DEPTH`- 
`MAX DEPTH`= 1
- 
`MAX DEPTH`= infinite
 
- 
- 
`KINDS`- select what kinds of entities you want to view, default is all kinds
- 
`RELATIONS`- select which relationships you want to view, default is all relationships
- 
`Direction`- orientation in which you want to view the entity and its associated nodes- Top to bottom
- Bottom to top
- Left to right
- Right to left
 
- 
`Curve`- 
`Curve`= Monotone
- 
`Curve`= Step Before
 
- 

You can also toggle:

- 
`Simplified`- On = simple view
- Off = detailed view
 
- 
`Merge relations`- On = You see the relationship from the selected entity to the nodes and from the nodes to the selected entity.
- Off = You only see relations from the selected entity to its nodes.
 The following graphics illustrate the view of the nodes and relationships, based on the combination of the settings of `Simplified`and`Merge relations`.- 
`Simplified`= On and`Merge Relations`= On
- 
`Simplified`= On and`Merge Relations`= Off
- 
`Simplified`= Off and`Merge Relations`= On
- 
`Simplified`= Off and`Merge Relations`= Off

# Citations

1. Source page: https://backstage.io/docs/getting-started/viewing-entity-relationships
