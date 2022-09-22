---
title: inigo delete
parent: Command Line Interface (CLI)
has_children: false
nav_order: 7
layout: page
---

# inigo create
---

## Commands
- [inigo delete service](#inigo-delete-service)
- [inigo delete access](#inigo-delete-access)
- [inigo delete rate_limit](#inigo-delete-rate_limit)
- [inigo delete security](#inigo-delete-security)

## Optional flags
* `help`, `h`
show help info

---

### ```inigo delete service```
#### **Description**
Deletes an existing service.

#### **Syntax**
```
inigo delete service [service_name]:[:label_name]
```

#### Optional flags
* `--label <value>`
deletes a service by a service label name
* `--help`, `-h`
show help info


#### **Output**
```
$ inigo delete service demo
```

---

### ```inigo delete access```
#### **Description**
Deletes an access configuration

#### **Syntax**
```
inigo delete access [service_name]:[:label_name]
```

#### Optional flags
* `--help`, `-h`
show help info
* `--label <value>`
deletes access configuration by a service label name
* `--wait-for <value>`
wait for particular number of instances to become updated (default: `0`)
* `--timeout <value>`
use timeout flag to interrupt execution if it exceeds timeout value (default: `0` seconds)
* `--wait`
wait for configuration to be applied to service instance (default: `false`)


#### **Output**
```
$ inigo delete access demo:starwars

demo:starwars/access removed
```

---

### ```inigo delete rate_limit```
#### **Description**
Deletes a rate limiting configuration.

#### **Syntax**
```
inigo delete rate_limit [service_name]:[:label_name]
```

#### Optional flags
* `--help`, `-h`
show help info
* `--label <value>`
deletes rate limiting configuration by a service label name
* `--wait-for <value>`
wait for particular number of instances to become updated (default: `0`)
* `--timeout <value>`
use timeout flag to interrupt execution if it exceeds timeout value (default: `0` seconds)
* `--wait`
wait for configuration to be applied to service instance (default: `false`)


#### **Output**
```
$ inigo delete rate_limit demo:starwars -h

demo:starwars/rate_limit removed
```


---

### ```inigo delete security```
#### **Description**
Deletes a security configuration.

#### **Syntax**
```
inigo delete security [service_name]:[:label_name]
```

#### Optional flags
* `--help`, `-h`
show help info
* `--label <value>`
deletes rate limiting configuration by a service label name
* `--wait-for <value>`
wait for particular number of instances to become updated (default: `0`)
* `--timeout <value>`
use timeout flag to interrupt execution if it exceeds timeout value (default: `0` seconds)
* `--wait`
wait for configuration to be applied to service instance (default: `false`)


#### **Output**
```
$ inigo delete security demo:starwars

demo:starwars/security removed
```

