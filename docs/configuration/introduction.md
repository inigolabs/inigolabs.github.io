---
title: Introduction
parent: Configuration
has_children: false
nav_order: 1
layout: page
---

# Table of Contents
- [Table of Contents](#table-of-contents)
- [Introduction](#introduction)

# Introduction
This section defines the format of Inigo's configuration files. Fields marked as `required` must be specified if the parent is defined.

All of Inigo's configuration files have global fields, the table below summarizes what the global fields are.

| Field | Type | Required | Description
| ---  | :---: | --- | --- |
| **kind** | `string` | Yes | The type of configuration file. Can be `RateLimit`, `Observe`, `Access`, `Security` or `Service`. |
| **name** | `string` | Yes | The name of the configuration file |
| **label** | `string` | No (default: `null`) | A descriptive label of the configuration file |
| **spec** | `object` | Yes | The specifications of the configuration file |

Every configuration file starts with these four fields. An example beginning of a configuration file for the `Security` kind can be seen below:

```
kind: Security
name: demo
label: starwars
spec:
  --snip--
  validation:
    alias_name: "^[a-zA-Z]+$"
  --snip--
```