---
sidebar_position: 1
---

# Deploy with Docker

:::danger

Astuto is still in early development, so these information may become outdated quickly and without notice. If you encounter any problems during installation, [open an issue](https://github.com/astuto/astuto/issues) on GitHub.

:::

## 0. Requirements

- Docker
- Docker Compose

## 1. Create a Docker Compose file

Create an empty folder and, inside that folder, create a file named `docker-compose.yml` with the following content:

```yml title="docker-compose.yml"
version: '3.4'
services:
  db:
    image: postgres:14.5
    environment:
      POSTGRES_USER: yourpostgresusername
      POSTGRES_PASSWORD: yourpostgrespassword
    volumes:
      - dbdata:/var/lib/postgresql/data
  web:
    image: riggraz/astuto:latest
    environment:
      POSTGRES_USER: yourpostgresusername
      POSTGRES_PASSWORD: yourpostgrespassword
      BASE_URL: http://yourwebsite.com
      SECRET_KEY_BASE: yoursecretkeybase
    ports:
      - "3000:3000"
    depends_on:
      - db
    
volumes:
  dbdata:
```

As it can be seen from the docker compose file, Astuto consists of two services: `web`, which contains the web application, and `db`, which contains a Postgres instance.

## 2. Edit the environment variables in the Docker Compose file

In `docker-compose.yml`, set the following environment variables to suit your needs:

| **Environment variable** | **Description**                                                                                          |
|--------------------------|----------------------------------------------------------------------------------------------------------|
| POSTGRES_USER            | Username for the Postgres database                                                                       |
| POSTGRES_PASSWORD        | Password for the Postgres database                                                                       |
| BASE_URL                 | The base URL from where the website will be served                                                       |
| SECRET_KEY_BASE          | A secure 64 characters secret (you can generate one from [this site](https://www.grc.com/passwords.htm)) |

:::caution

Remember to set `POSTGRES_USER` and `POSTGRES_PASSWORD` in both services (`web` and `db`)!

:::

## 3. Run

Run the following command:
```sh
docker compose pull && docker compose up
```

You should now have a running instance of Astuto on port 3000. A default user account has been created with credentials email: `admin@example.com`, password: `password`.

:::caution Permission denied on Linux

If you are on Linux and you encounter permission denied errors when running Docker commands, try to run them as administrator.

:::