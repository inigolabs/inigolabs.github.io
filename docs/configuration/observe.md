---
title: Observe
parent: Configuration
has_children: false
nav_order: 6
layout: page
---

# Table of Content
- [Table of Content](#table-of-content)
- [Observe](#observe)
  - [Field Tags](#field-tags)
  - [Directive Tags](#directive-tags)
  - [Profiles](#profiles)
  - [Profile Default Values](#profile-default-values)

# Observe
Observe allows Inigo's users to perform inspection of queries and annotate certain parts of it depending on the configuration you set. For example, you may use Observe to mark/flag fields used in a query depending on the types of directives are applied to them in your GraphQL schema.

---

This section defines the format of Inigo's `Observe` type configuration files. Fields marked as `required` must be specified if the parent is defined.

## Field Tags

| Field | Type | Required | Description
| ---  | :---: | --- | --- |
| `field_tags[_].type` | `string` | Yes | The GraphQL Type |
| `field_tags[_].field` | `string` | Yes | The GraphQL Field |
| `field_tags[_].tag` | `string` | Yes | A tag value |

```
kind: Observe
name: demo
label: starwars
spec:
  field_tags:
    - type: Film
      field: director
      tag: sensitive
```

## Directive Tags

| Field | Type | Required | Description
| ---  | :---: | --- | --- |
| `directive_tags` | `array` | No | List of GraphQL Directives inigo searches for to flag use of deprecated fields |

In the example below, inigo will signal in the response that a deprecated field `Film.director` was used in the query if the corresponding schema includes the `deprecated` directive in the `director` field. This functionality is not limited to field deprecation, any directive string can be used in the context of your application. For example, using security-related directives such as `pii` or `internal` could also work.

```
kind: Observe
name: demo
label: starwars
spec:
  field_tags:
    - type: Film
      field: director
      tag: sensitive
  directive_tags:
    - deprecated
```

## Profiles

| Field | Type | Required | Description
| ---  | :---: | --- | --- |
| `profiles[_].name` | `string` | Yes | The name of the profile. |
| `profiles[_].deprecated_extension` | `boolean` | No (default: `false`) | Show selected deprecated fields within the response's `extensions` key. |

In the example configuration below, an Observe configuration will be applied to the `anonymous` profile, and deprecated fields will not be shown to this profile.

```
kind: Observe
name: demo
label: starwars
spec:
  profiles:
  - name: anonymous
    deprecated_extension: false
```

## Profile Default Values
All toggles from the [Profiles](#profiles) section can be applied using a default profile by specifying the `profile_default_values` property, as shown below.

| Field | Type | Required | Description
| ---  | :---: | --- | --- |
| `profile_default_values` | `object` | No | Default observe profile configuration settings. |


```
kind: Observe
name: demo
label: starwars
spec:
  profile_default_values:
    deprecated_extension: false
```