---
type: Web Page
title: Enabling a public entry point | Backstage Software Catalog and Developer Platform
description: A guide for how to experiment with public and protected Backstage app
  bundles
resource: https://backstage.io/docs/tutorials/enable-public-entry
timestamp: '2026-07-06T13:23:17.605783+00:00'
---

This documentation is written for the new frontend system, which is the default in new Backstage apps. If your Backstage app still uses the old frontend system, read the old frontend system version of this guide instead.

# Enable Public Entry (Experimental)

In this tutorial, you will learn how to restrict access to your main Backstage app bundle to authenticated users only.

It is expected that the protected bundle feature will be refined in future development iterations, but for now, here is a simplified explanation of how it works:

Your Backstage app bundle is split into two code entries:

- Public entry point containing login pages;
- There is also a protected main entry point that contains the code for what you see after signing in.

With that, Backstage's cli and backend will detect public entry point and serve it to unauthenticated users, while serving the main, protected entry point only to authenticated users.

## Requirements

- The app needs to be served by the `app-backend`plugin, or this won't work;
- Also it will only work for those using `backstage-cli`to build and serve their Backstage app.

## Step-by-step

- 
Create a `index-public-experimental.tsx`in your app`src`folder.noteThe filename is a convention, so it is not currently configurable. 
- 
This file is the public entry point for your application, and it should only contain what unauthenticated users should see: in packages/app/src/index-public-experimental.tsx`import ReactDOM from 'react-dom/client';`
 import { signInPageModule } from './overrides/SignInPage';
 import { appModulePublicSignIn } from '@backstage/plugin-app/alpha';
 import { createApp } from '@backstage/frontend-defaults';
 const app = createApp({
 features: [signInPageModule, appModulePublicSignIn],
 });
 ReactDOM.createRoot(document.getElementById('root')!).render(
 app.createRoot(),
 );The `signInPageModule`is your custom sign-in page extension that you should already have configured in your app. The`appModulePublicSignIn`from`@backstage/plugin-app/alpha`provides the`CookieAuthRedirect`component that triggers an authenticated redirect to the main app after sign-in.noteThe frontend will handle cookie refreshing automatically, so you don't have to worry about it. 
- 
Let's verify that everything is working locally. From your project root folder, run the following commands to build the app and start the backend: `# building the app package`
 yarn workspace app start
 # starting the backend api
 yarn start-backend
- 
Visit http://localhost:7007 to see the public app and validate that the *index.html*response only contains a minimal application.noteRegular app serving will always serve protected apps without authenticating. 
- 
Finally, as soon as you log in, you will be redirected to the main app home page (inspect the page and see that the protected bundle was served from the app backend after the redirect). 

That's it!

# Citations

1. Source page: https://backstage.io/docs/tutorials/enable-public-entry
