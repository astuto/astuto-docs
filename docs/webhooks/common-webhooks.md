---
sidebar_position: 2
---

# Common Webhooks

This page contains tutorials for configuring some common webhook integrations.

## Slack

In this tutorial, we are going to create a webhook that automatically sends a message to a Slack channel every time a new feedback is submitted to Astuto. However, there are many more Slack integrations you can create (e.g. by changing the Slack endpoint URL or the webhook's trigger).

:::info Slack API documentation
To further customize your Slack integration or create new ones, we suggest to read [Slack REST API](https://api.slack.com/web) for a comprehensive list of endpoints and parameters.
:::

To create a webhook for Slack integration, we need to create a Slack app and add it to a Slack workspace.

1. Navigate to [Slack API Dashboard](https://api.slack.com/apps), click "Create New App", choose "From scratch", fill "App Name" and choose the app's workspace
2. In the page of your newly created Slack app, on the left sidebar, click "OAuth & Permissions" and add the `chat:write` permission under "Scopes > Bot Token Scopes"
3. Click "Install App to Workspace" and grant authorization to the app
4. Copy the "Bot User OAuth Token" and store it in a safe place
5. Navigate to your Slack worskpace. In the left sidebar, right click on the channel you want to send messages to and click "View channel details". Take note of "Channel ID".
6. Navigate to your Astuto feedback space, then go to "Site settings > Webhooks" and click "New"
7. Fill the form with the following values and click "Save":
    - **Name**: a name of your choice
    - **Description**: a description of your choice (optional)
    - **Trigger**: "New post" (you can change it to suit your needs)
    - **HTTP method**: POST
    - **URL**: `https://slack.com/api/chat.postMessage`
    - **HTTP body**: (change to suit your needs)
      ```
      {
        "channel": <ID of your Slack Channel>,
        "text": "{{ post_author.full_name }} posted new feedback '{{ post.title | escape_json }}'! Link: {{ post.url }}"
      }
      ```
    - **Header 1 key**: `Content-Type`
    - **Header 1 value**: `application/json; charset=utf-8`
    - **Header 2 key**: `Authorization`
    - **Header 2 value**: `Bearer <Your Bot User OAuth Token>`
8. [Test](./webhooks-introduction.md#test-your-webhook) your newly configured webhook. If everything is okay, you can Enable the webhook.

## Trello

In this tutorial, we are going to create a webhook that automatically creates a new Trello Card in a specific Trello List every time a new feedback is submitted to Astuto. However, there are many more Trello integrations you can create (e.g. by changing the Trello endpoint URL or the webhook's trigger).

:::info Trello API documentation
To further customize your Trello integration or create new ones, we suggest to read [Trello REST API](https://developer.atlassian.com/cloud/trello/rest) for a comprehensive list of endpoints and parameters.
:::

To create a webhook for Trello integration, we need to create a Trello Power-Up.

1. Navigate to [Trello Power-Up Dashboard](https://trello.com/power-ups/admin) and click "New"
2. Fill the following fields: "New Power-Up or Integration", "Workspace", "Email", "Support Contact" and "Author"; then click "Create"
3. If not already there, navigate to the "API key" page through the left sidebar, then click "Generate a new API key". Take note of the "API key".
4. Navigate to the following URL, replacing `<POWER_UP_NAME>` and `YOUR_API_KEY` with the chosen Power-Up name and generated API key: `https://trello.com/1/authorize?expiration=never&name=<POWER_UP_NAME>&scope=read,write&response_type=token&key=<YOUR_API_KEY>`
5. A page should appear that asks for your permission to add the newly created Power-Up to your account. Click "Allow".
6. A new page with a token should appear. Take note of the token.
7. Navigate to your Trello Board. Click on a Card of the List you want to send Astuto feedback to. From the Card, on the right sidebar, click "Share > Export JSON". Take note of the "idList" in the JSON.
8. Navigate to your Astuto feedback space, then go to "Site settings > Webhooks" and click "New"
9. Fill the form with the following values and click "Save":
    - **Name**: a name of your choice
    - **Description**: a description of your choice (optional)
    - **Trigger**: "New post" (you can change it to suit your needs)
    - **HTTP method**: POST
    - **URL**: `https://api.trello.com/1/cards?key=<API_KEY>&token=<TOKEN>` (substitute `<API_KEY>` and `<TOKEN>` with your specific values)
    - **HTTP body**: (change to suit your needs)
      ```
      {
        "name": "{{ post.title | escape_json }}",
        "desc": "{{ post.description | escape_json }}",
        "urlSource": "{{ post.url }}",
        "idList": "<YOUR_ID_LIST>"
      }
      ```
    - **Header 1 key**: `Content-Type`
    - **Header 1 value**: `application/json`
10. [Test](./webhooks-introduction.md#test-your-webhook) your newly configured webhook. If everything is okay, you can Enable the webhook.

## GitHub

In this tutorial, we are going to create a webhook that automatically creates a new GitHub issue in a specific GitHub repository every time a new feedback is submitted to Astuto. However, there are many more GitHub integrations you can create (e.g. by changing the GitHub endpoint URL or the webhook's trigger).

:::info GitHub API documentation
To further customize your GitHub integration or create new ones, we suggest to read [GitHub REST API](https://docs.github.com/en/rest/quickstart) for a comprehensive list of endpoints and parameters.
:::

To create a webhook for GitHub integration, we need to create a GitHub personal access token (PAT).

1. Navigate to GitHub [Developer Settings](https://github.com/settings/apps), click "Personal access tokens" and then click "Fine-grained tokens"
2. Click "Generate new token"
3. Fill in the following fields: "Token name", "Resource owner", "Expiration", "Repository access", "Permissions". In particular, under "Permissions > Repository permissions", set access of "Issues" to "Read and Write".
4. Click "Generate token" and take note of the personal access token generated
5. Navigate to your Astuto feedback space, then go to "Site settings > Webhooks" and click "New"
6. Fill the form with the following values and click "Save":
    - **Name**: a name of your choice
    - **Description**: a description of your choice (optional)
    - **Trigger**: "New post" (you can change it to suit your needs)
    - **HTTP method**: POST
    - **URL**: `https://api.github.com/repos/<OWNER>/<REPOSITORY>/issues`
    - **HTTP body**: (change to suit your needs)
      ```
      {
        "title": "{{ post.title | escape_json }}",
        "body": "{{ post.description | escape_json }}"
      }
      ```
    - **Header 1 key**: `Authorization`
    - **Header 1 value**: `Bearer <YOUR_TOKEN>`
    - **Header 2 key**: `accept`
    - **Header 2 value**: `application/vnd.github+json`
    - **Header 3 key**: `X-GitHub-Api-Version`
    - **Header 3 value**: `2022-11-28`
