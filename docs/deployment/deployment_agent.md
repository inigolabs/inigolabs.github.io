---
title: Agent
parent: Deployment
has_children: false
nav_order: 1
layout: page
---

# Table of Contents
- [Table of Contents](#table-of-contents)
  - [Getting Started](#getting-started)


Getting Started
-----

1. Download the inigo agent binary from the [releases page](https://github.com/inigolabs/artifacts/releases), or use one of the platform dependant package managers.
    - MacOS:
      ``` sh
      > brew tap inigolabs/homebrew-tap
      > brew install inigo_agent
      ```
    - Linux:
      ```
      ```
    - Windows:
      ```
      // TODO
      ```
2. Create a `config.yml` file containing the Egress URL and Service Token
    ``` yaml
      EgressURL: https://localhost:4000/query
      ServiceToken: "PUT YOUR SERVICE TOKEN HERE"
    ```
    > Head over to the [runtime configuration documentation](deployment_runtime_override.html) to learn how to customize the daemon. 
3. Set correct the binary permissions with `chmod +x` and execute the binary.