---
type: Web Page
title: Transitioning to the New JSX Transform | Backstage Software Catalog and Developer
  Platform
description: A guide to migrating your project to the New JSX Transform
resource: https://backstage.io/docs/tutorials/jsx-transform-migration
timestamp: '2026-07-06T13:23:17.605783+00:00'
---

# Transitioning to the New JSX Transform

Backstage core libraries currently support React 18. We are actively evaluating the upgrade to React 19, which introduces significant changes, including making the New JSX Transform mandatory.

## What this means for you

- **If you are already using the New JSX Transform:**You are not impacted by this change, regardless of your React version (17, 18, or when 19 becomes available for Backstage).
- **If you are NOT using the New JSX Transform (likely if you're importing React like**You will need to adopt it before upgrading to React 19. This typically involves changing your imports, as the New JSX Transform doesn't require importing the entire React namespace to use JSX. This is recommended even on React 17 or 18, as it was a change introduced with React 17. Although a best practice since React 17, Backstage did not adopt this transform when it upgraded.- `import React from 'react'`):

## Action Required

While upgrading to React 19 within Backstage is not yet officially supported, it's recommended to proactively adopt the New JSX Transform if you haven't already. This will ensure a smoother transition when React 19 support is introduced and improve compatibility with the current React ecosystem.

## Timeline

We are currently evaluating React 19 and will provide further guidance on the upgrade path and timelines soon. For now, you can prepare by adopting the New JSX Transform.

## Migration Process

### Updating React Imports

Find and replace all occurrences of `import * as React from 'react'` and `import React from 'react'` with named imports like:

```
import { useState, useEffect } from 'react';
```
If you must preserve the default React import for compatibility reasons, you can use:

```
import { default as React } from 'react';
```
To streamline this process, consider using an automated codemod.

### Updating Configuration Files

To ensure compatibility when using `@backstage/cli`, you must update your `tsconfig.json` to use the new JSX transforms.

#### TypeScript Configuration (TSConfig)

Update the `compilerOptions.jsx` setting in `tsconfig.json` to `react-jsx`. This file is typically located in the root directory.

```
{
  "extends": "@backstage/cli/config/tsconfig.json",
  ...
  "compilerOptions": {
    "jsx": "react",
    "jsx": "react-jsx"
  }
}
```
In the future, this setting will change to `preserve` once React 17 is fully deprecated.

##### Explanation of `compilerOptions.jsx` Values

- 
The `react`mode: This mode converts JSX into`React.createElement`calls, making it directly usable by React. The code doesn't require a separate JSX transformation step, and the output files will use the`.js`extension.
- 
The `react-jsx`mode: Introduced with React 17, this mode automatically handles the JSX transformation, allowing you to use JSX without needing to import`React`in each file.
- 
The `preserve`mode: This option leaves the JSX code untouched, embedding it directly into the output files. This is useful when you're planning to process the JSX with another tool like Babel later. The resulting files will use the`.jsx`extension to indicate the presence of JSX.

# Citations

1. Source page: https://backstage.io/docs/tutorials/jsx-transform-migration
