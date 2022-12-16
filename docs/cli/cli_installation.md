---
title: Installation
parent: Command Line Interface (CLI)
has_children: false
nav_order: 1
layout: page
---

# Installation
--------------

Use brew to easily install the cli and make it easy to upgrade to the latest release in the future.  
If brew is not available in your system, head over to our [artifacts](https://github.com/inigolabs/artifacts/releases/latest) page get the right executable for your system. 

### MacOS or Linux (brew)
- First time install:
   ```
   brew tap inigolabs/homebrew-tap
   brew install inigo_cli
   ```

- Upgrade to the latest version
   ```
   brew upgrade inigo_cli
   ```
- If you don't have `brew` you can install it from [here](https://brew.sh/).

### From Executable
- Download and install the binary for you system [here](https://github.com/inigolabs/artifacts/releases/latest).

## Test Run
Make sure you everything is working by running the `inigo` command. 

```
$ inigo -h
NAME:
   inigo - Inigo CLI

USAGE:
   inigo [global options] command [command options] [arguments...]

VERSION:
   v0.17.3 : 2022-12-07T07:18:51Z : 8e475c58

COMMANDS:
   login    login
   logout   logout
   apply    apply a configuration file
   create   create a resource
   delete   delete a resource
   get      get info for a particular resource
   check    check [entity]
   help, h  Shows a list of commands or help for one command

GLOBAL OPTIONS:
   --debug        Run with debugging info (default: false)
   --help, -h     show help (default: false)
   --version, -v  print the version (default: false)
```

