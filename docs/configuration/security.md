---
title: Security
parent: Configuration
has_children: false
nav_order: 3
layout: page
---

[//]: # ( Code generated by inigolabs.com/m/libs/confgen, DO NOT EDIT. )

Security
========

Security allows Inigo's users to enforce security controls before they reach your GraphQL server. Inigo's security enforcement allows you to mitigate Denial of Service attacks, as well as the abuse of your API which could overwhelm your application's resources.

---

This section defines the format of Inigo's `Security` type configuration files. Fields marked as `required` must be specified if the parent is defined.

Spec
----

| Field                     | Type                                                          | Description                                                                     |
|---------------------------|---------------------------------------------------------------|---------------------------------------------------------------------------------|
| validation                | [ValidationConfig](#validationconfig)                         |                                                                                 |
| allow_http_get_operations | boolean `default:true`                                        | Clients are allowed to query GraphQL using HTTP GET (in addition to HTTP POST). |
| profile_default_values    | [SecurityProfileDefaultValues](#securityprofiledefaultvalues) |                                                                                 |
| profiles                  | \[[SecurityProfile](#securityprofile)] `required`             |                                                                                 |

ValidationConfig
----------------

| Field          | Type                                                    | Description                                               |
|----------------|---------------------------------------------------------|-----------------------------------------------------------|
| alias_name     | string                                                  | Regular expression to validate query alias names.<br>     |
| directive_name | string                                                  | Regular expression to validate query directive names.<br> |
| operation_name | string                                                  | Regular expression to validate the operation name.<br>    |
| arguments      | [ArgumentsValidationConfig](#argumentsvalidationconfig) |                                                           |

ArgumentsValidationConfig
-------------------------

| Field  | Type   | Description                                                                |
|--------|--------|----------------------------------------------------------------------------|
| String | string | Regular expression to validate GraphQL query arguments of String type.<br> |

SecurityProfileDefaultValues
----------------------------

| Field                   | Type                  | Description                                                                                                                     |
|-------------------------|-----------------------|---------------------------------------------------------------------------------------------------------------------------------|
| max_depth               | int                   | Maximum length limit for queries.                                                                                               |
| max_height              | int                   | Maximum query height limit for queries.                                                                                         |
| max_directives          | int                   | Maximum number of query directives allowed in a query (both existent and non-existent query directives).<br>                    |
| max_request_size_bytes  | int `default:512000`  | Maximum client request size allowed in bytes.                                                                                   |
| max_response_size_bytes | int `default:2048000` | Maximum server response size allowed in bytes.                                                                                  |
| max_root_queries        | int                   | Number of allowed root queries in a single query.                                                                               |
| max_root_mutations      | int                   | Number of allowed root mutations in a single query.                                                                             |
| require_operation_name  | boolean               | Requires queries to have an operation name set.                                                                                 |
| pii                     | [string] `required`   | One of:<br>- `SSN`<br>- `CreditCard`                                                                                            |
| require_fields          | object                | Mandates the use of specific fields when some type is used in a query.<br><br>require_fields:<br> User: [ name, email ]<br><br> |
| require_id_fields       | boolean               | Requires query selection sets to have an id field where it exists.                                                              |
| max_aliases             | int                   | Maximum allowed aliased fields in a query.                                                                                      |

SecurityProfile
---------------

| Field                   | Type                  | Description                                                                                                                     |
|-------------------------|-----------------------|---------------------------------------------------------------------------------------------------------------------------------|
| Name                    | string `required`     | Name of the profile.                                                                                                            |
| max_depth               | int                   | Maximum length limit for queries.                                                                                               |
| max_height              | int                   | Maximum query height limit for queries.                                                                                         |
| max_directives          | int                   | Maximum number of query directives allowed in a query (both existent and non-existent query directives).<br>                    |
| max_request_size_bytes  | int `default:512000`  | Maximum client request size allowed in bytes.                                                                                   |
| max_response_size_bytes | int `default:2048000` | Maximum server response size allowed in bytes.                                                                                  |
| max_root_queries        | int                   | Number of allowed root queries in a single query.                                                                               |
| max_root_mutations      | int                   | Number of allowed root mutations in a single query.                                                                             |
| require_operation_name  | boolean               | Requires queries to have an operation name set.                                                                                 |
| pii                     | [string] `required`   | One of:<br>- `SSN`<br>- `CreditCard`                                                                                            |
| require_fields          | object                | Mandates the use of specific fields when some type is used in a query.<br><br>require_fields:<br> User: [ name, email ]<br><br> |
| require_id_fields       | boolean               | Requires query selection sets to have an id field where it exists.                                                              |
| max_aliases             | int                   | Maximum allowed aliased fields in a query.                                                                                      |
