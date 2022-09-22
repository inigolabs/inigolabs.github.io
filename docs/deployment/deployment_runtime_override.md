---
title: Overriding Runtime Configuration
parent: Deployment
has_children: false
nav_order: 4
layout: page
---

# Table of Contents
- [Table of Contents](#table-of-contents)
- [Runtime Configuration](#runtime-configuration)
  - [Configuration Table](#configuration-table)

# Runtime Configuration
Using environment variables, you can customize certain functionalities of the Inigo daemon service, such as the port number, the log level, and other aspects. The table below shows the available toggles and buttons of the daemon.

When you need to override any runtime defaults, you will export your environment variable and set it to the correct value. For example: `export INIGO_LOG_LEVEL=debug`.

## Configuration Table

| Description | Type | Required | Details | Environment Variable
| ---  | :---: | --- | --- | --- |
| Log Level | `string` | No (default: `info`)| Log-level for the daemon. | `INIGO_LOG_LEVEL` |
| Log Type | `string` | No (default: `json`)| Log-type for the daemon. | `INIGO_LOG_TYPE` |
| Listen Port | `integer` | No (default: `80`)| TCP port to bind the daemon to. | `INIGO_LISTEN_PORT` |
| Egress URL | `string` | Yes | URL of the proxied application (GraphQL Endpoint). | `INIGO_EGRESS_URL` |
| Service Token | `string` | Yes | JWT token credential of the service. | `INIGO_SERVICE_TOKEN` |
| GraphQL Route | `string` | No (default: `/query`)| Endpoint route for GraphQL queries. | `INIGO_GRAPHQL_ROUTE` |
| GraphQL Playground Route | `string` | No | Endpoint route for GraphQL IDE (GraphiQL or GraphQL Playground). | `INIGO_PLAYGROUND_ROUTE` |
| Sidecar JWT Secret | `string` | No | Sidecar authentication JWT secret. | `INIGO_SIDECAR_JWT_SECRET` |


