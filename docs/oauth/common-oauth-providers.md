---
sidebar_position: 3
---

# Common OAuth Providers

This page contains tutorials for configuring some common OAuth providers.

## Google

1. Navigate to https://console.developers.google.com and create a new project
2. Using the left sidebar, navigate to "API and services" and then to "Credentials"
3. Click "Create Credentials" and then click "OAuth client ID"
4. Choose "Web application" as "Application type", type the name of your application and click "Create"
5. Take note of the "Client ID" and "Client secret" shown
6. On Astuto, navigate to "Site Settings > Authentication" and click "New"
7. Fill the form with the following values and click "Save":
   - **Name**: Google
   - **Client ID**: the Client ID you took note of
   - **Client Secret**: the Client Secret you took note of
   - **Authorize URL**: `https://accounts.google.com/o/oauth2/v2/auth`
   - **Token URL**: `https://accounts.google.com/o/oauth2/token`
   - **Scope**: `https://www.googleapis.com/auth/userinfo.email https://www.googleapis.com/auth/userinfo.profile`
   - **Profile URL**: `https://www.googleapis.com/oauth2/v2/userinfo`
   - **JSON path to user email**: `email`
   - **JSON path to user name**: `name`
8. On Astuto, navigate to "Site Settings > Authentication" and click "Copy URL" next to the Google OAuth
9. On Cloud Console, edit the newly created OAuth Client
10. Under "Authorised redirect URIs", click "Add URI", paste the copied URL and click "Save"
11. On Astuto, [test](./oauth-configuration-basics.md#oauth-test) the newly configured provider

## Facebook

1. Navigate to https://developers.facebook.com/apps/creation/, create a new project and follow the instructions
2. Then, from your project dashboard, in the lower left corner, click "App settings" and then "Basic"
3. Take note of the "App ID" and "App secret"
4. On Astuto, navigate to "Site Settings > Authentication" and click "New"
5. Fill the form with the following values and click "Save":
   - **Name**: Facebook
   - **Client ID**: the App ID you took note of
   - **Client Secret**: the App Secret you took note of
   - **Authorize URL**: `https://www.facebook.com/v19.0/dialog/oauth`
   - **Token URL**: `https://graph.facebook.com/v19.0/oauth/access_token`
   - **Scope**: `email`
   - **Profile URL**: `https://graph.facebook.com/v19.0/me?fields=email,name`
   - **JSON path to user email**: `email`
   - **JSON path to user name**: `name`
6. On Astuto, navigate to "Site Settings > Authentication" and click "Copy URL" next to the Facebook OAuth
7. Then, from your Facebook project dashboard, in the left sidebar, click "Use cases" and, on the right of "Authentication and account creation", click the "Customize" button
8. Add "email" under "Permissions" if not already activated
9. Click "Go to settings" button
10. In "Valid OAuth Redirect URIs" paste the copied URL and click "Save changes"
11. On Astuto, [test](./oauth-configuration-basics.md#oauth-test) the newly configured provider

## Discord

1. Navigate to https://discord.com/developers/applications and click "New Application"
2. Type the name of your application (e.g. "Astuto"), accept the terms of service and click "Create"
3. Using the left sidebar, navigate to "OAuth2 > General"
4. Take note of the "Application ID" shown
5. Click "Reset Secret" and take note of the "Client Secret" shown
6. On Astuto, navigate to "Site Settings > Authentication" and click "New"
7. Fill the form with the following values and click "Save":
   - **Name**: Discord
   - **Client ID**: the Application ID you took note of
   - **Client Secret**: the Client Secret you took note of
   - **Authorize URL**: `https://discord.com/oauth2/authorize`
   - **Token URL**: `https://discord.com/api/oauth2/token`
   - **Scope**: `email identify`
   - **Profile URL**: `https://discord.com/api/users/@me`
   - **JSON path to user email**: `email`
   - **JSON path to user name**: `username`
8. On Astuto, navigate to "Site Settings > Authentication" and click "Copy URL" next to the Discord OAuth
9. On Discord, navigate again to "OAuth2 > General"
10. Click "Add Redirect", paste the copied URL and click "Save"
11. On Astuto, [test](./oauth-configuration-basics.md#oauth-test) the newly configured provider

## GitHub

:::info This is an advanced configuration

If you don't understand what's going on in the following configuration, you may want to take a look at the [advanced OAuth configuration instructions](./oauth-configuration-advanced.md#requesting-user-data-from-multiple-endpoints).

:::

1. Navigate to https://github.com/settings/developers and click "New OAuth App"
2. Type the name of your application (e.g. "Astuto")
3. Type your homepage URL
4. Since we do not have a callback URL yet, enter the homepage URL again. We will edit it later.
5. Click "Register application"
6. Click "Generate client secret", then take note of "Client ID" and "Client secret"
7. On Astuto, navigate to "Site Settings > Authentication" and click "New"
8. Fill the form with the following values and click "Save":
   - **Name**: GitHub
   - **Client ID**: the Client ID you took note of
   - **Client Secret**: the Client Secret you took note of
   - **Authorize URL**: `https://github.com/login/oauth/authorize`
   - **Token URL**: `https://github.com/login/oauth/access_token`
   - **Scope**: `user`
   - **Profile URL**: `https://api.github.com/user/emails;https://api.github.com/user`
   - **JSON path to user email**: `profile0[0].email`
   - **JSON path to user name**: `profile1.name`
9. On Astuto, navigate to "Site Settings > Authentication" and click "Copy URL" next to the GitHub OAuth
10. On GitHub, on the OAuth page, scroll all the way down. Paste the copied URL to "Authorization callback URL"
11. Click "Update application"
12. On Astuto, [test](./oauth-configuration-basics.md#oauth-test) the newly configured provider

## Microsoft Entra ID (Azure AD)

1. Navigate to https://aad.portal.azure.com/ and find "Manage -> App registrations"
2. Click "New registration"
3. Type the name of your application (e.g. "Astuto")
4. Choose which kind of users allowed to login. Select Single tenant, if you only need to provide access to users in our organisation
5. The Redirect URI will entered later
6. Click "Register"
7. On the new application frontpage take note of the "Application ID" and "Directory (Tenant) ID" shown
8. Also click the "Endpoints" link at the top, where you can view the Authorize URL and Token URL.
9. Navigate to "Certificates & secrets" in left menu and click "New Client Secret"
10. Give the new created secret a description and set an expire date.
11. Click "Add" and note the secret value. It cannot be displayed again.
12. On Astuto, navigate to "Site Settings > Authentication" and click "New"
13. Fill the form with the following values and click "Save":
   - **Name**: Microsoft
   - **Client ID**: the Application ID you took note of
   - **Client Secret**: the Client Secret you took note of
   - **Authorize URL**: `https://login.microsoftonline.com/<TenantID>/oauth2/v2.0/authorize`
   - **Token URL**: `https://login.microsoftonline.com/<TenantID>/oauth2/v2.0/token`
   - **Scope**: `openid`
   - **Profile URL**: `https://graph.microsoft.com/oidc/userinfo`
   - **JSON path to user email**: `email`
   - **JSON path to user name**: `name`
14. On Astuto, navigate to "Site Settings > Authentication" and click "Copy URL" next to the Microsoft OAuth
15. On Microsoft Entra, navigate again the created app registration in click on "Authentication"
16. Click "Add platform", and choose "web" and paste the copied URL into Redirect URIs and click "Configure"
17. On Astuto, [test](./oauth-configuration-basics.md#oauth-test) the newly configured provider
