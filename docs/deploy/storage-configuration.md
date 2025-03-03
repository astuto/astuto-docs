---
sidebar_position: 3
slug: /storage-configuration
---

# Storage Configuration

Astuto allows users to attach images to their feedback and administrators to change site logo and favicon. When an image is uploaded to Astuto, by default it is stored in the local disk storage. You can change this default behavior and specify, for example, an external cloud storage in which to store attachments.

Astuto supports every S3-compatible cloud storage services. Examples are: Amazon S3, DigitalOcean Spaces, Wasabi.

:::caution Migrating from local storage to cloud storage, and vice versa

Migrating from local storage to cloud storage or vice versa will likely break your currently uploaded attachments, so we highly recommend against it! When setting up your Astuto instance, you should decide upfront whether you want your uploads to be stored on your server disk or in an external cloud provider.

:::

Below you can find a `docker-compose.yml` configuration to set up your external cloud storage provider:

```yml title="docker-compose.yml"
services:
  db:
    image: postgres:14.5
    environment: &db-env
      POSTGRES_USER: astuto
      POSTGRES_PASSWORD: dbpass
    volumes:
      - dbdata:/var/lib/postgresql/data
  web:
    build:
      context: .
      dockerfile: Dockerfile
      target: dev
    environment:
      <<: *db-env
      BASE_URL: http://localhost:3000
      SECRET_KEY_BASE: secretkeybasehere

      S3_ENDPOINT: <endpoint-of-your-cloud-storage-provider>
      S3_BUCKET: <name-of-bucket>
      S3_ACCESS_KEY_ID: <access-key-id>
      S3_ACCESS_KEY_SECRET: <access-key-secret>
      ACTIVE_STORAGE_PUBLIC_SERVICE: s3_public
      ACTIVE_STORAGE_PRIVATE_SERVICE: s3_private
    ports:
      - "3000:3000"
    depends_on:
      - db

volumes:
  dbdata:
```

Configure variables `S3_ENDPOINT`, `S3_BUCKET`, `S3_ACCESS_KEY_ID` and `S3_ACCESS_KEY_SECRET` with the correct values for your cloud storage provider. Leave `ACTIVE_STORAGE_PUBLIC_SERVICE` and `ACTIVE_STORAGE_PRIVATE_SERVICE` as is: by default, Astuto will mark site logo and favicon, user avatars and OAuth logos as publicly accessible images (so they can be cached), whereas it will mark post and comment attached images as private.


:::caution Uploading images returns error 413, Request Entity Too Large

This probably happens because your nginx configuration blocks request with a body that is considered too big. You should increase the body size limit to something around 20MB. You can do so by updating your nginx.conf file: under http { ... } add directive "client_max_body_size 20M;".

:::