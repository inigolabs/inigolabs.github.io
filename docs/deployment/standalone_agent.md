---
title: Standalone Agent
parent: Deployment
has_children: false
nav_order: 1
layout: page
---

# Standalone Agent

### Installation

Download the inigo agent binary for your platform from the [artifacts](https://github.com/inigolabs/artifacts/releases) page.

### Basic Configuration

Configuring the agent can be done using a yaml config file and or using environment variables.  
The following basic configuration is required:
  ``` yaml
    EgressURL: https://localhost:4000/query
    ServiceToken: "YOUR-INIGO-SERVICE-TOKEN"
  ```
2. Set correct the binary permissions with `chmod +x` and execute.

### Other Configuration
Using environment variables, you can customize certain functionalities of the agent, such as the port number, the log level, and other aspects. The table below shows the available toggles and buttons of the agent.

When you need to override any runtime defaults, you will export your environment variable and set it to the correct value. For example: `export INIGO_LOG_LEVEL=debug`.

## Configuration Table

| Description | Type | Required | Details | Environment Variable | YAML Config
| ---  | :---: | --- | --- | --- | --- |
| Log Level | `string` | No (default: `info`)| Log-level for the daemon. | `INIGO_LOG_LEVEL` | `LogLevel` |
| Log Type | `string` | No (default: `json`)| Log-type for the daemon. | `INIGO_LOG_TYPE` | `LogType` |
| Listen Port | `integer` | No (default: `80`)| TCP port to bind the daemon to. | `INIGO_LISTEN_PORT` | `ListenPort` |
| Egress URL | `string` | Yes | URL of the proxied application (GraphQL Endpoint). | `INIGO_EGRESS_URL` | `EgressURL` |
| Service Token | `string` | Yes | JWT token credential of the service. | `INIGO_SERVICE_TOKEN` | `ServiceToken` |
| GraphQL Route | `string` | No (default: `/query`)| Endpoint route for GraphQL queries. | `INIGO_GRAPHQL_ROUTE` | `GraphQLRoute` |
| GraphQL Playground Route | `string` | No | Endpoint route for GraphQL IDE (GraphiQL or GraphQL Playground). | `INIGO_PLAYGROUND_ROUTE` | `GraphQLPlaygroundRoute` |
| Sidecar JWT Secret | `string` | No | Sidecar authentication JWT secret. | `INIGO_SIDECAR_JWT_SECRET` |



4. Head over to the [runtime configuration documentation](deployment_runtime_override.html) to learn how to customize the agent. 