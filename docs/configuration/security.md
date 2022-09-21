---
title: Security
parent: Configuration
has_children: false
nav_order: 2
layout: page
---

# Table of Contents
- [Table of Contents](#table-of-contents)
- [Security](#security)
  - [Validation](#validation)
  - [Profiles](#profiles)
  - [Profile Default Values](#profile-default-values)

# Security
Security allows Inigo's users to enforce security controls before they reach your GraphQL server. Inigo's security enforcement allows you to mitigate Denial of Service attacks, as well as the abuse of your API which could overwhelm your application's resources.

---

This section defines the format of Inigo's `Security` type configuration files. Fields marked as `required` must be specified if the parent is defined.

## Validation

| Field | Type | Required | Description
| ---  | :---: | --- | --- |
| `validation.alias_name` | `string` | No | Regular expression to validate query alias names. |
| `validation.directive_name` | `string` | No | Regular expression to validate query directive names. |
| `validation.operation_name` | `string` | No | Regular expression to validate the operation name. |
| `validation.arguments` | `object` | No | Regular expression to validate GraphQL query arguments of **String** type. For example: `String`:`^[a-zA-Z]+$`. |


## Profiles

| Field | Type | Required | Description
| ---  | :---: | --- | --- |
| `profiles[_].name` | `string` | Yes | The name of the profile. |
| `profiles[_].max_depth` | `int` | No (default: unlimited) | Maximum length limit for queries. |
| `profiles[_].max_height` | `int` | No (default: unlimited) | Maximum query height limit for queries. |
| `profiles[_].max_directives` | `int` | No (default: unlimited) | Maximum number of query directives allowed in a query (both existent and non-existent query directives). |
| `profiles[_].max_aliases` | `int` | No (default: unlimited) | Maximum allowed aliased fields in a query. |
| `profiles[_].max_request_size_bytes` | `int` | No (default: `512000` bytes) | Maximum client request size allowed in bytes. |
| `profiles[_].max_response_size_bytes` | `int` | No (default: `2048000` bytes) | Maximum server response size allowed in bytes. |
| `profiles[_].max_root_queries` | `int` | No (default: unlimited) | Number of allowed root queries in a single query. |
| `profiles[_].max_root_mutations` | `int` | No (default: unlimited) | Number of allowed root mutations in a single query. |
| `profiles[_].allow_http_get_operations` | `boolean` | No (default: `true`) | Clients are allowed to query GraphQL using HTTP `GET` (in addition to HTTP `POST`) |
| `profiles[_].require_operation_name` | `boolean` | No (default: `true`) | Requires queries to have an operation name set. |
| `profiles[_].require_fields` | `array[object]` | No (default: `null`) | Mandates the use of specific fields when some type is used in a query. For example, `User`: [`name`,`email`]. |
| `profiles[_].require_id_fields` | `boolean` | No (default: `false`) | Requires query selection sets to have an `id` field where it exists. |

The **Security** configuration below is an example config that does regex-based validation, as well as applies security features on the **guest** profile

```
kind: Security
name: demo
label: starwars
spec:
  validation:
    alias_name: ^[a-zA-Z]+$
    directive_name: ^[a-zA-Z]+$
    operation_name: ^[a-zA-Z]+$
    arguments:
      string: ^[a-zA-Z]+$

  profiles:
    - name: guest
      max_depth: 3
      max_height: 9
      max_directives: 5
      max_request_size_bytes: 512000
      max_response_size_bytes: 2048000
      max_root_queries: null
      max_root_mutations: null
      require_operation_name: true
      allow_http_get_operations: false

    - name: admin
      max_depth: 5
      max_height: 100
      max_directives: null
      max_request_size_bytes: 512000
      max_response_size_bytes: 2048000
      max_root_queries: null
      max_root_mutations: null
      require_operation_name: false
      require_id_fields: false
      require_fields:
        User: [name, email]
```


## Profile Default Values
All toggles from the [Profiles](#profiles) section can be applied using a default profile by specifying the `profile_default_values` property, as shown below.

| Field | Type | Required | Description
| ---  | :---: | --- | --- |
| `profile_default_values` | `object` | No | Default security profile configuration settings. |

```
kind: Security
name: demo
label: starwars
spec:
  profile_default_values:
    ...
    require_id_fields: false
    require_operation_name: true
    ...
```