---
sidebar_position: 2
---

# Common OAuth Providers

This page contains tutorials for configuring some common OAuth providers.

## Discord

1. Navigate to https://discord.com/developers/applications and click on "New Application"
2. Type the name of your application (e.g. "Astuto"), accept the terms of service and click "Create"
3. Using the left sidebar, navigate to "OAuth2 > General"
4. Take note of the "Application ID" shown
5. Click on "Reset Secret" and take note of the "Client Secret" shown
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
   - **JSON path to user name**: name
8. On Astuto, navigate to "Site Settings > Authentication" and click on "Copy URL" next to the Discord OAuth
9. On Discord, navigate again to "OAuth2 > General"
10. Click on "Add Redirect", paste the copied URL and click "Save"
11. On Astuto, [test](./oauth-configuration-basics.md#oauth-test) the newly configured provider