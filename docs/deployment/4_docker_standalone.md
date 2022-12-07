---
title: Docker Standalone
parent: Deployment
has_children: false
nav_order: 4
layout: page
---

# Docker Standalone

  ``` sh
  $ docker run -d \
    -e INIGO_EGRESS_URL="http://localhost:4000/query" \
    -e INIGO_SERVICE_TOKEN="PUT YOUR SERVICE TOKEN HERE" \
    -p 80:80 inigohub/sidecar
  ```

  **Note:** Make sure to replace `http://localhost:4000/query` with your target service endpoint.

  > Head over to the [runtime configuration documentation](deployment_runtime_override.html) to learn more about the available environment variables.
