---
sidebar_position: 1
slug: /deploy-docker
---

# Deploy with Docker

:::info Want to avoid deployment and maintenance?

Try Astuto paid plan! You get a 7-day free trial without entering any payment method, then you pay as little as 15 €/month with annual subscription. [**Learn more**](https://astuto.io/?utm_campaign=docs_deploy&utm_source=docs.astuto.io) or [**start your 7-day trial now**](https://login.astuto.io/signup).

:::

## 0. Requirements

- Docker
- Docker Compose

## 1. Create a Docker Compose file

Create an empty folder and, inside that folder, create a file named `docker-compose.yml` with the following content:

```yml title="docker-compose.yml"
services:
  db:
    image: postgres:14.5
    environment: &db-env
      POSTGRES_USER: postgresusername
      POSTGRES_PASSWORD: postgrespassword
    volumes:
      - dbdata:/var/lib/postgresql/data

  web:
    image: riggraz/astuto:latest
    environment:
      <<: *db-env
      BASE_URL: http://yourwebsite.com
      SECRET_KEY_BASE: yoursecretkeybase
    ports:
      - "3000:3000"
    depends_on:
      - db
    
volumes:
  dbdata:
```

## 2. Edit environment variables

In `docker-compose.yml`, set the following environment variables to suit your needs:

| **Environment variable**  | **Service** | **Description**                                                                                                                                                                 |
|---------------------------|-------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| POSTGRES_USER             | db, web     | Username for the Postgres database                                                                                                                                              |
| POSTGRES_PASSWORD         | db, web     | Password for the Postgres database                                                                                                                                              |
| POSTGRES_HOST             | web         | Container name of the Postgres database. Default value is 'db'                                                                                                                                              |
| BASE_URL                  | web         | The base URL from where the website will be served                                                                                                                              |
| SECRET_KEY_BASE           | web         | A secure 64 characters secret (you can generate one from [this site](https://www.grc.com/passwords.htm))                                                                        |
| ACTIVE_JOB_BACKEND        | web         | Which job scheduler to use for background jobs (optional, possible values: "sidekiq" or "async", defaults to "async"). To setup Sidekiq, see [this page](/deploy-with-sidekiq). |
| EMAIL_DELIVERY_METHOD     | web         | Possible values: "smtp". If you don't want to configure an email delivery method, don't define this variable.                                                                   |
| EMAIL_SMTP_HOST           | web         | Hostname of your SMTP server                                                                                                                                                    |
| EMAIL_SMTP_PORT           | web         | Port of your SMTP server (optional, defaults to: 25)                                                                                                                            |
| EMAIL_SMTP_USER           | web         | Username for your SMTP server (optional, don't define this variable if your SMTP server doesn't require authentication)                                                         |
| EMAIL_SMTP_PASS           | web         | Password for your SMTP server (optional, don't define this variable if your SMTP server doesn't require authentication)                                                         |
| *other SMTP variables...* |             | A full list of environment variables for email configuration and other helpful tips can be found at [this link](/smtp-configuration)                                            |
| RAILS_LOG_TO_STDOUT       | web         | Whether to log to stdout or not. Useful for debugging purposes. (optional, defaults to false in production)                                                                     |

## 3. Run

Run the following command:
```sh
docker compose pull && docker compose up
```

You should now have a running instance of Astuto on port 3000. A default user account has been created with credentials email: `admin@example.com`, password: `password`.

:::caution Permission denied on Linux

If you are on Linux and you encounter permission denied errors when running Docker commands, try to run them as administrator.

:::
