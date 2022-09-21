---
title: CLI
parent: Installation
has_children: false
nav_order: 3
layout: page
---

# Table of Contents
- [Table of Contents](#table-of-contents)
- [Inigo CLI](#inigo-cli)
  - [Installation](#installation)
    - [MacOS and Linux](#macos-and-linux)
    - [Executable](#executable)
  - [Usage and Documentation](#usage-and-documentation)


# Inigo CLI

---

Inigo CLI, or `inigo`, is a command line interface that allows your to manage your GraphQL service configurations, for use in the command line or CI/CD pipelines.

## Installation

### MacOS and Linux
1. Install the tap
`brew tap inigolabs/homebrew-tap`

2. Install the CLI
`brew install inigo_cli`

3. Make sure you are able to run it `inigo -h`

```
$ inigo -h

NAME:
   inigo - Inigo CLI

USAGE:
   inigo [global options] command [command options] [arguments...]

VERSION:
   v0.14.0 : 2022-09-14T21:28:02Z : b764a19e
```

If you don't have Brew, you can install it from [here](https://brew.sh/).

### Executable
Download and install the binary for you system [here](https://github.com/inigolabs/cli/releases/latest).

## Usage and Documentation
All `inigo` CLI documentation live [here](../../Usage/CLI/inigo.html).