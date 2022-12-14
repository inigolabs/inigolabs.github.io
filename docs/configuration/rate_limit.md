---
title: Rate Limit
parent: Configuration
has_children: false
nav_order: 5
layout: page
---

[//]: # ( Code generated by inigolabs.com/m/libs/confgen, DO NOT EDIT. )

Rate Limit
==========

Rate Limit configuration allows Inigo's users to apply fine-grained traffic controls. Not all clients are the same; you may have authenticated and unauthenticated clients using your application. Using the rate limit capability of inigo, you can enforce rate limiting policies depending on the authentication and authorization context of your clients.

---

This section defines the format of Inigo's `RateLimit` type configuration files. Fields marked as `required` must be specified if the parent is defined.

Spec
----

| Field                  | Type                                                            | Description |
|------------------------|-----------------------------------------------------------------|-------------|
| profile_default_values | [RateLimitProfileDefaultValues](#ratelimitprofiledefaultvalues) |             |
| profiles               | \[[RateLimitProfile](#ratelimitprofile)] `required`             |             |

RateLimitProfileDefaultValues
-----------------------------

| Field            | Type                                                          | Description                                                                                         |
|------------------|---------------------------------------------------------------|-----------------------------------------------------------------------------------------------------|
| extension_output | boolean                                                       | Adds rate limit-related information to the `extensions` response JSON key named `rate_limiter`.<br> |
| calls            | \[[RateLimitCallConfig](#ratelimitcallconfig)] `required`     |                                                                                                     |
| credits          | \[[RateLimitCreditConfig](#ratelimitcreditconfig)] `required` |                                                                                                     |

RateLimitCallConfig
-------------------

| Field     | Type                                      | Description                                                                                                       |
|-----------|-------------------------------------------|-------------------------------------------------------------------------------------------------------------------|
| path      | string `required`                         |                                                                                                                   |
| allowance | string&nbsp;&#124;&nbsp;number `required` | Can be either regular number or string with one of the following prefixes 'k', 'M'. <br><br>Example: 1k, 20M.<br> |
| period    | string `required`                         | String represents the duration in the form "72h3m0.5s".<br>                                                       |

RateLimitCreditConfig
---------------------

| Field     | Type                                      | Description                                                                                                       |
|-----------|-------------------------------------------|-------------------------------------------------------------------------------------------------------------------|
| period    | string `required`                         | String represents the duration in the form "72h3m0.5s".<br>                                                       |
| allowance | string&nbsp;&#124;&nbsp;number `required` | Can be either regular number or string with one of the following prefixes 'k', 'M'. <br><br>Example: 1k, 20M.<br> |

RateLimitProfile
----------------

| Field            | Type                                                          | Description                                                                                         |
|------------------|---------------------------------------------------------------|-----------------------------------------------------------------------------------------------------|
| Name             | string `required`                                             | Name of the profile.                                                                                |
| extension_output | boolean                                                       | Adds rate limit-related information to the `extensions` response JSON key named `rate_limiter`.<br> |
| calls            | \[[RateLimitCallConfig](#ratelimitcallconfig)] `required`     |                                                                                                     |
| credits          | \[[RateLimitCreditConfig](#ratelimitcreditconfig)] `required` |                                                                                                     |

RateLimitCallConfig
-------------------

| Field     | Type                                      | Description                                                                                                       |
|-----------|-------------------------------------------|-------------------------------------------------------------------------------------------------------------------|
| path      | string `required`                         |                                                                                                                   |
| allowance | string&nbsp;&#124;&nbsp;number `required` | Can be either regular number or string with one of the following prefixes 'k', 'M'. <br><br>Example: 1k, 20M.<br> |
| period    | string `required`                         | String represents the duration in the form "72h3m0.5s".<br>                                                       |

RateLimitCreditConfig
---------------------

| Field     | Type                                      | Description                                                                                                       |
|-----------|-------------------------------------------|-------------------------------------------------------------------------------------------------------------------|
| period    | string `required`                         | String represents the duration in the form "72h3m0.5s".<br>                                                       |
| allowance | string&nbsp;&#124;&nbsp;number `required` | Can be either regular number or string with one of the following prefixes 'k', 'M'. <br><br>Example: 1k, 20M.<br> |
