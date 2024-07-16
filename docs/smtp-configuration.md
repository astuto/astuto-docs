---
sidebar_position: 3
slug: /smtp-configuration
---

# SMTP Configuration

This page provides information on configuring Astuto to work with a SMTP server. Some simple examples will be shown alongside possible problems that might arise. In the end, a full list of available environment variables for SMTP configuration is provided.

:::info Get insightful logs about email delivery

During initial SMTP configuration, you may find it useful to set the environment variables `EMAIL_RAISE_DELIVERY_ERRORS` and `RAILS_LOG_TO_STDOUT` both to `true`. This will make Astuto print useful logs regarding email delivery. After testing that your configuration works, you can remove these environment variables or set them to `false`.

:::

## Examples

### SMTP server (with authentication)

Set the following environment variables:

```
EMAIL_DELIVERY_METHOD=smtp
EMAIL_SMTP_HOST=your.smtp.host
EMAIL_SMTP_PORT=25
EMAIL_SMTP_USER=your_smtp_user
EMAIL_SMTP_PASS=your_smtp_pass
```

:::info Try `login` over `plain`

If you get an error with the above configuration, it may be that your SMTP server doesn't support the `plain` authentication method (which is used by default by Astuto). Try to set the additional environment variable `EMAIL_SMTP_AUTH` to `login`.

:::

### SMTP server (without authentication, not recommended) 

If you plan on using a SMTP server without any authentication, then set the following environment variables (**note**: don't define `EMAIL_SMTP_USER` and `EMAIL_SMTP_PASS` at all):

```
EMAIL_DELIVERY_METHOD=smtp
EMAIL_SMTP_HOST=your.smtp.host
EMAIL_SMTP_PORT=25
```

## SMTP environment variables

The following table contains all the available environment variables you can set to configure SMTP. All these environment variable must be set on the `web` Docker service only.

| **Environment variable**       | **Description**                                                                                                     |
|--------------------------------|---------------------------------------------------------------------------------------------------------------------|
| EMAIL_DELIVERY_METHOD          | [See here](/deploy-docker/#2-edit-the-environment-variables-in-the-docker-compose-file)                             |
| EMAIL_SMTP_HOST                | [See here](/deploy-docker/#2-edit-the-environment-variables-in-the-docker-compose-file)                             |
| EMAIL_SMTP_PORT                | [See here](/deploy-docker/#2-edit-the-environment-variables-in-the-docker-compose-file)                             |
| EMAIL_SMTP_USER                | [See here](/deploy-docker/#2-edit-the-environment-variables-in-the-docker-compose-file)                             |
| EMAIL_SMTP_PASS                | [See here](/deploy-docker/#2-edit-the-environment-variables-in-the-docker-compose-file)                             |
| EMAIL_RAISE_DELIVERY_ERRORS    | Whether to log information about email delivery. Useful for debugging purposes (optional, defaults to: false)       |
| EMAIL_SMTP_AUTH                | SMTP server authentication type (optional, defaults to: plain, available values: plain, login)                      |
| EMAIL_MAIL_FROM                | Set default MAIL_FROM email (optional, defaults to: noreply@astuto.io)                                              |
| EMAIL_MAIL_REPLY_TO            | Set default REPLY_TO email (optional, defaults to: noreply@astuto.io)                                               |
| EMAIL_SMTP_HELO_DOMAIN         | HELO domain (optional)                                                                                              |
| EMAIL_SMTP_STARTTLS_AUTO       | Detects if STARTTLS is enabled in your SMTP server and starts to use it (optional, default: true)                   |
| EMAIL_SMTP_TLS                 | Enables the SMTP connection to use SMTP/TLS (optional)                                                              |
| EMAIL_SMTP_OPENSSL_VERIFY_MODE | [See here](https://guides.rubyonrails.org/configuring.html#config-action-mailer-smtp-settings) for more information |