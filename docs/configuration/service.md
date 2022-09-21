---
title: Service
parent: Configuration
has_children: false
nav_order: 5
layout: page
---

# Table of Contents
- [Table of Contents](#table-of-contents)
- [Service](#service)
  - [Request](#request)
  - [Daemon (sidecar) Settings](#daemon-sidecar-settings)

# Service
Service configuration allows Inigo's users to apply fine-grianed authorization and access controls. Not all clients are the same; you may have authenticated and unauthenticated clients using your application. Using the access control capabilities of Inigo, you can enforce strong authorization controls depending on the context of your clients.

---

This section defines the format of Inigo's `Service` type configuration files. Fields marked as `required` must be specified if the parent is defined.


## Request

| Field | Type | Required | Description
| ---  | :---: | --- | --- |
| `path_trace_id` | `string` | No | Path to the Trace ID header. |
| `path_user_profile` | `string` | No | Path to a user profile header. For JWT headers, you can use `jwt.user_profile` or `jwt.<some_path_to_user_profile_key>`. |
| `path_user_role` | `string` | No | Path to a user role header. For JWT headers, you can use `jwt.roles` or `jwt.<some_path_to_user_roles_key>`. |
| `path_user_id` | `string` | No | Path to a user ID header. For JWT headers, you can use `jwt.user_id` or `jwt.<some_path_to_user_id_key>`. |
| `path_client_info` | `string` | No | Path to the client version header. |


## Daemon (sidecar) Settings

| Field | Type | Required | Description |
| `polling_interval_schema` | `int` | No (default: `300`) | Interval (in seconds) to poll the GraphQL schema from the application. |
| `polling_interval_profile` | `int` | No (default: `10`) | Interval (in seconds) to poll new configurations. |
| `enable_extensions_output` | `boolean` | No default (`true`)| Enable the exposure of the GraphQL `extensions` response key. |
| `anonymous_profile` | `string` (default: `anonymous`)| No | Name of an anonymous profile. |
| `anonymous_roles` | `array[string]` | No | List of roles that are considered anonymous. |
| `schema_files` | `array[string]` | No | Relative path to the filesystem location of your files containing GraphQL schemas. For example: `../../schemas/prod.graphql`. |
| `reduce_extension_output` | `array[string]` | No | List of `extensions` JSON keys to reduce from the response. |
| `failure_mode` | `string` | No | Default action to take upon failure mode. Options: `open` (Pass failed requests to the service), `block` (blocks failed requests from reaching the service), `query_only` (same as `open`, but only for queries of root type *query*).  |

The example service configuration below shows how a service can be defined.

```
kind: Service
name: demo
label: starwars
spec:
  path_user_profile: jwt.user_profile
  path_user_role: jwt.user_roles
  path_user_id: jwt.user_name

  anonymous_profile: guest
  anonymous_roles:
    - viewer

  polling_interval_schema: 300
  polling_interval_profile: 2

  enable_extensions_output: true
  reduce_extension_output:
    - trace

  failure_mode: query_only
  schema_files:
    - ../../schemas/prod.graphql
```