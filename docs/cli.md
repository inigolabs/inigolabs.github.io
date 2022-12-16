---
title: Command Line Interface (CLI)
has_children: true
nav_order: 6
layout: page
---

# Command Line Interface
------------------------

Inigo CLI, or `inigo`, is a command line interface that allows your to manage your GraphQL service configurations.  
The CLI can be used in any terminal or can be integrated into your CI/CD pipelines.  
With the CLI, you can perform actions such as creating new services, applying new configurations, and viewing currently applied service configurations.  
If you are familiar with kubernetes kubectl command, you'll feel right at home using the Inigo cli. 

### Commands
- [inigo login](commands/login.html)
- [inigo logout](commands/logout.html)
- [inigo apply](commands/apply.html)
- [inigo create](commands/create.html)
- [inigo delete](commands/delete.html)
- [inigo get](commands/get.html)
- [inigo check](commands/check.html)

### Optional flags
* `--debug`
show verbose debug information
* `--help`, `-h`
show help info
* `--version`, `-v`
show version info