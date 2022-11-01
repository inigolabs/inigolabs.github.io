---
title: Docker
parent: Deployment
has_children: false
nav_order: 2
layout: page
---

# Table of Contents
- [Table of Contents](#table-of-contents)
  - [Prerequisites](#prerequisites)
  - [Docker](#docker)
  - [Docker-compose](#docker-compose)

Prerequisites
-----

- A working Docker instance. If not, see the [Docker website](http://www.docker.io/gettingstarted/#h_installation) for installation instructions.
- A working GraphQL Server instance.


Docker
-----

  **Note:** Make sure to replace `http://localhost:4000/query` with your target service endpoint.

  ``` sh
  $ docker run -d \
    -e INIGO_EGRESS_URL="http://localhost:4000/query" \
    -e INIGO_SERVICE_TOKEN="PUT YOUR SERVICE TOKEN HERE" \
    -p 80:80 inigohub/sidecar
  ```

  > Head over to the [runtime configuration documentation](deployment_runtime_override.html) to learn more about the available environment variables.


Docker-compose
-----

  **Note:** this code snippet includes a starwars graphql example instance, make sure to replace with your own service.

  1. Create a `docker-compose.yml` file

      ``` yaml
      version: "3.9"
      services:
        starwars: # example instance
          image: inigohub/starwars
          
        sidecar:
          image: inigohub/sidecar
          ports:
            - 80:80
          # env_file: .env
          environment:
            INIGO_EGRESS_URL: http://starwars:80/query # Make sure to configure
            INIGO_SERVICE_TOKEN: "PUT YOUR SERVICE TOKEN HERE" # This can be stored in an .env file instead
            INIGO_GRAPHQL_ROUTE: /query
            INIGO_QUERYDATABATCH_MAX_TIME: 5s
            INIGO_QUERYDATABATCH_MAX_COUNT: "50"
      ```

      > Head over to the [runtime configuration documentation](deployment_runtime_override.html) to learn more about the available environment variables.

  2. Run the services
      ``` sh
      $ docker-compose up -d
      ```