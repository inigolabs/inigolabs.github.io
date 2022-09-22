---
title: inigo check
parent: Command Line Interface (CLI)
has_children: false
nav_order: 4
layout: page
---

# inigo check
---

## Commands
- [inigo check access](#inigo-check-access)
- [inigo check schema](#inigo-check-schema)

## Optional flags
* `help`, `h`
show help info

---

### ```inigo check access```
#### **Description**
Check access prints out any errors or issues with the current access configuration for a given service.

#### **Syntax**
```
inigo check access [service_name][:label_name]
```

#### Optional flags
* `--label`
checks access by a service label name
* `--help`, `-h`
show help info


#### **Output**
```
$ inigo check access demo:starwars

demo/access/role/viewer  ok
demo/access/role/director  ok
demo/access/role/actor  ok
demo/access/role/producer  ok
```

---

### ```inigo check schema```
#### **Description**
Check for breaking schema changes. The check schema command will check wether the supplied schema has any breaking changes. The command uses analytics data from the last 30 days to see if any removed or updated fields will result in broken clients.

#### **Syntax**
```
inigo check schema [service_name] [schema_files...]
```

#### Optional flags
* `--help`, `-h`
show help info


#### **Output**
```
$ inigo check schema demo:starwars ../../schema.graphql
```