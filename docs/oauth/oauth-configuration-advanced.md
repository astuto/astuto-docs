---
sidebar_position: 2
---

# OAuth Configuration Advanced

This page explains some advanced techniques for configuring OAuth providers.

## Requesting user data from multiple endpoints

Occasionally, some OAuth providers (e.g. GitHub) may return the user email from an endpoint and the username from a different endpoint.

In these particular cases, you can specify multiple Profile URLS: just separate them with a semicolon (`;`). Astuto will make a request to each of these endpoints and return a single JSON object with keys `profile0` (for the first profile URL provided), `profile1` (for the second profile URL provided), and so on. Each of this profile contains the response from the respective profile URL.

For example, if you [configure GitHub as written in the documentation](./common-oauth-providers.md#github), you will get back the following JSON object:

```json
{
  "profile0": [
    {
      "email": "riccardo.graziosi97@gmail.com",
      "primary": true,
      "verified": true,
      "visibility": "private"
    }
  ],
  "profile1": {
    "login": "riggraz",
    "name": "Riccardo Graziosi",
    "company": null,
    "blog": "https://riggraz.dev/",
    ...
}
```

Then, you can use the JSON path to user email and username to get the data you need!