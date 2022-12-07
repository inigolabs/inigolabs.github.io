---
title: Docker
parent: Deployment
has_children: false
nav_order: 5
layout: page
---

# Docker Compose

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
      ```

      > Head over to the [runtime configuration documentation](deployment_runtime_override.html) to learn more about the available environment variables.

  2. Run the services
      ``` sh
      $ docker-compose up -d
      ```