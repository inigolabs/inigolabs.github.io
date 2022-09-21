---
title: Access
parent: Configuration
has_children: false
nav_order: 3
layout: page
---

# Table of Contents
- [Table of Contents](#table-of-contents)
- [Access](#access)
  - [Roles](#roles)
  - [Profiles](#profiles)
  - [Profile Default Values](#profile-default-values)

# Access
Access configuration allows Inigo's users to apply fine-grained authorization and access controls. Not all clients are the same; you may have authenticated and unauthenticated clients using your application. Using the access control capabilities of Inigo, you can enforce strong authorization controls depending on the context of your clients.

---

This section defines the format of Inigo's `Access` type configuration files. Fields marked as `required` must be specified if the parent is defined.

## Roles

| Field | Type | Required | Description
| ---  | :---: | --- | --- |
| `roles[_].name` | `string` | Yes | The name of the role. |
| `roles[_].full_access` | `boolean` | No (default: `true`) | Grants full schema access to the role. This setting takes presedence and over any access configuration files. |
| `roles[_].config_files` | `array[string]` | No (default: `null`) | Relative path to the filesystem location of your access files. For example: `access_files/viewer.inigo`. |
| `roles[_].allowed_operations` | `array[string]` | No (default: `null`) | Relative path to the filesystem location of your files containing allowed operations. For example: `allowed_operations/viewer.graphql`. |

## Profiles

| Field | Type | Required | Description
| ---  | :---: | --- | --- |
| `profiles[_].name` | `string` | Yes | The name of the role. |
| `profiles[_].introspection_mode` | `string` | No (default: `full`) | Introspection mode policy for the given profile. Options are: `full`, `partial` or `block`. |

The example below define a **viewer** role with access policies, and an profile access profile that `block`s introspection to guest users.

```
kind: Access
name: demo
label: starwars
spec:
  roles:
    - name: viewer
      config_files:
        - access/viewer.inigo
      allowed_operations:
        - access/viewer.graphql

  profiles:
    - name: guest
      introspection_mode: block
```

In this example, the config file (`config_files`) `access/viewer.inigo` is as follows:
```
query {
  login
  logout
  films {
    director
    producer
    title
    characters {
      name
      appearedIn
    }
  }
  people
}

type Film {
    title
    director
    characters
    producer
}

type Person {
    name
    birthYear
    height
    ssn
}
```


The allowed operations (`allowed_operations`) file `access/viewer.graphql` is as follows:
```
query Planets {
  planets {
    name
    appearedIn {
      title
    }
}

```


## Profile Default Values
All toggles from the [Profiles](#profiles) section can be applied using a default profile by specifying the `profile_default_values` property, as shown below.

| Field | Type | Required | Description
| ---  | :---: | --- | --- |
| `profile_default_values` | `object` | No | Default access profile configuration settings. |

