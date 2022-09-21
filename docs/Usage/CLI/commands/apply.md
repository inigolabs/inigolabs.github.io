---
title: inigo apply
parent: Command Line Interface (CLI)
grand_parent: Usage
has_children: false
nav_order: 6
layout: page
---

# inigo apply
---

## Commands
- [inigo apply](#inigo-apply)

## Optional flags
* `--help`, `-h`
show help info
* `--label <value>`
applies configuration by a service label name
* `--wait-for <value>`
wait for particular number of instances to become updated (default: `0`)
* `--timeout <value>`
use timeout flag to interrupt execution if it exceeds timeout value (default: `0` seconds)
* `--wait`
wait for configuration to be applied to service instance (default: `false`)

---

### ```inigo apply```
#### **Description**
Apply a configuration to a service.
Configuration yaml files can be passed in individually or using a glob to apply multiple configuration files at once.

#### **Syntax**
```
inigo apply <config_filename>
```

#### Optional flags
* `--label <value>`
applies a configuration by service label
* `--help`, `-h`
show help info


#### **Output**
```
$ inigo apply *.yml

demo:starwars/service updated
demo:starwars/access/profiles/guest updated
```
The command will print out the status of the changes applied to a configuration, such as *created*, *updated* or *removed*.