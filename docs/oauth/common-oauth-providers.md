---
sidebar_position: 2
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
   - **Authorize URL**: https://accounts.google.com/o/oauth2/v2/auth
   - **Token URL**: https://accounts.google.com/o/oauth2/token
   - **Scope**: https://www.googleapis.com/auth/userinfo.email https://www.googleapis.com/auth/userinfo.profile
   - **Profile URL**: https://www.googleapis.com/oauth2/v2/userinfo
   - **JSON path to user email**: email
   - **JSON path to user name**: name
8. On Astuto, navigate to "Site Settings > Authentication" and click "Copy URL" next to the Google OAuth
9. On Cloud Console, edit the newly created OAuth Client
10. Under "Authorised redirect URIs", click "Add URI", paste the copied URL and click "Save"
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
   - **Authorize URL**: https://discord.com/oauth2/authorize
   - **Token URL**: https://discord.com/api/oauth2/token
   - **Scope**: email
   - **Profile URL**: https://discord.com/api/users/@me
   - **JSON path to user email**: email
   - **JSON path to user name**: username
8. On Astuto, navigate to "Site Settings > Authentication" and click "Copy URL" next to the Discord OAuth
9. On Discord, navigate again to "OAuth2 > General"
10. Click "Add Redirect", paste the copied URL and click "Save"
11. On Astuto, [test](./oauth-configuration-basics.md#oauth-test) the newly configured provider
