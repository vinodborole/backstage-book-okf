---
type: Web Page
title: Validate your OpenAPI spec against test data | Backstage Software Catalog and
  Developer Platform
description: Documentation on how to use the `repo schema openapi test` command.
resource: https://backstage.io/docs/openapi/test-case-validation
timestamp: '2026-07-06T13:23:17.605783+00:00'
---

# Validate your OpenAPI spec against test data

## OpenAPI Validation using Test Cases

This is primarily performed by `backstage-repo-tools repo schema openapi test`. Any errors found in the generated specs can be either

- Fixed manually, this is usually relevant for request body or response body changes.
- Fixed automatically with `backstage-repo-tools repo schema openapi test --update`.
- Fixing the test case. This can happen where a response is mocked as

```
it('should return the right value', () => {
  // We will assume that this is the actual response and update the spec accordingly.
  // Ideally, this should be a fully populated return value.
  const entity: Entity = {} as any;
  app.get('/test', () => {
    return entity;
  });
  const response = await request(app).get('/test');
  expect(response.body).toEqual(entity);
});
```
will cause an invalid spec validation. The return value doesn't have all properties as defined in the type. Try to avoid this if possible. Something better would be,

```
it('should return the right value', () => {
  // We will assume that this is the actual response and update the spec accordingly.
  // Ideally, this should be a fully populated return value.
  const entity: Entity = {
    apiVersion: 'a1',
    kind: 'k1',
    metadata: { name: 'n1' },
  };
  app.get('/test', () => {
    return entity;
  });
  const response = await request(app).get('/test');
  expect(response.body).toEqual(entity);
});
```
Additionally, for more advanced use cases, you can run `yarn optic capture {PATH_TO_OPENAPI_FILE} --update interactive` and go through the prompts on the screen. Under the hood, the test validation + updating is done by Optic, a great project around supporting OpenAPI specs and development. You can find additional options here.

# Citations

1. Source page: https://backstage.io/docs/openapi/test-case-validation
