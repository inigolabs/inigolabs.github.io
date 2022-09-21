---
title: Rate Limit
parent: Configuration
has_children: false
nav_order: 4
layout: page
---

# Table of Contents
- [Table of Contents](#table-of-contents)
- [Rate Limit](#rate-limit)
  - [Profiles](#profiles)
  - [Profile Default Values](#profile-default-values)

# Rate Limit
Rate Limit configuration allows Inigo's users to apply fine-grained traffic controls. Not all clients are the same; you may have authenticated and unauthenticated clients using your application. Using the rate limit capability of inigo, you can enforce rate limiting policies depending on the authentication and authorization context of your clients.

---

This section defines the format of Inigo's `RateLimit` type configuration files. Fields marked as `required` must be specified if the parent is defined.

## Profiles

| Field | Type | Required | Description
| ---  | :---: | --- | --- |
| `profiles[_].name` | `string` | Yes | The name of the profile. |
| `profiles[_].header_output` | `boolean` | No (default: `false`) | Adds rate limit-related information to the HTTP response header. Rate limit-related headers will be prefixed with `X-RateLimit...`. |
| `profiles[_].extension_output` | `boolean` | No (default: `false`) | Adds rate limit-related information to the `extensions` response JSON key named `rate_limiter`. |
| `profiles[_].calls_per_minute` | `int` (default: unlimited) | No | Number of queries allowed per minute. |
| `profiles[_].calls_per_hour` | `int` | No (default: unlimited) | Number of queries allowed per hour. |
| `profiles[_].credits_per_minute` | `int` | No (default: unlimited) | Credit allowance per minute. |
| `profiles[_].credits_per_hour` | `int` | No (default: unlimited) | Credit allowance per hour. |
| `profiles[_].credits_per_type` | `object` | No (default: unlimited) | Credits spent when a GraphQL type is used in a query. For example: `Film`:`2`. |
| `profiles[_].credits_per_root_field` | `object` | No (default: `1`) | Credits spent when a GraphQL root field is used in a query. For example: `login`:`15`. You can use `credits_per_root_field` to override rate limiting such that specific fields are not rate limited by setting the field to zero (`0`). |

The rate limit configuration below shows how to apply a configuration to multiple profiles, such as **guest**, **user** and **admin**.

```
kind: RateLimit
name: demo
label: starwars
spec:
  profile_default_values:
    calls_per_minute: 10
    credits_per_minute: 1000

  profiles:
  - name: guest
    header_output: true
    extension_output: true
    calls_per_hour: 100000
    credits_per_hour: 100000
    credits_per_root_field:
      login: 15
    credit_per_type:
      Film: 2
      Person: 10

  - name: admin
    calls_per_minute: 10
    credits_per_minute: 1000

  - name: user
    calls_per_minute: 10
    credits_per_minute: 1000
```


## Profile Default Values
All toggles from the [Profiles](#profiles) section can be applied using a default profile by specifying the `profile_default_values` property, as shown below.

| Field | Type | Required | Description
| ---  | :---: | --- | --- |
| `profile_default_values` | `object` | No | Default rate limit profile configuration settings. |
