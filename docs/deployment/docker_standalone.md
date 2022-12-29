---
title: Docker Standalone
parent: Deployment
has_children: false
nav_order: 4
layout: page
---

# Docker Standalone
-------------------

  ``` sh
  $ docker run -d \
    -e INIGO_EGRESS_URL="http://localhost:4000/query" \
    -e INIGO_SERVICE_TOKEN="YOUR-INIGO-SERVICE-TOKEN" \
    -p 80:80 inigohub/sidecar
  ```

  **Note:** Make sure to replace `http://localhost:4000/query` with your target service endpoint.

  > Head over to the [Configuration documentation](https://docs.inigo.io/docs/configuration.html) to learn more about the available environment variables.
 
