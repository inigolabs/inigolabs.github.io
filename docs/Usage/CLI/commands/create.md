---
title: inigo create
parent: Command Line Interface (CLI)
grand_parent: Usage
has_children: false
nav_order: 3
layout: page
---

# inigo create
---

## Commands
- [inigo create service](#inigo-create-service)
- [inigo create demo](#inigo-create-demo)
- [inigo create token](#inigo-create-token)

## Optional flags
* `help`, `h`
show help info

---

### ```inigo create service```
#### **Description**
Creates a new service.

#### **Syntax**
```
inigo create service [service_name]:[:label_name]
```

#### Optional flags
* `--label <value>`
sets a label value for a service
* `--init`
create service with default config files (default: `false`)
* `--help`, `-h`
show help info


#### **Output**
```
$ inigo create service demo:test

service 3606503789527040 created

$ inigo create service dolev:test1 --init

service 3606571775000576 created
```

---

### ```inigo create demo```
#### **Description**
Creates a demo service.

#### **Syntax**
```
inigo create demo
```

#### Optional flags
* `--help`, `-h`
show help info


#### **Output**
```
$ inigo create demo

created inigo_starwars_demo/access/actor.inigo
created inigo_starwars_demo/access/director.inigo
created inigo_starwars_demo/access/producer.inigo
created inigo_starwars_demo/access/viewer.graphql
created inigo_starwars_demo/access/viewer.inigo
created inigo_starwars_demo/access.yml
created inigo_starwars_demo/rate_limit.yml
created inigo_starwars_demo/security.yml
created inigo_starwars_demo/service.yml
```

---

### ```inigo create token```
#### **Description**
Creates a service token.

#### **Syntax**
```
inigo create token [service_name]:[:label_name]
```

#### Optional flags
* `--label`
creates a token by service label name
* `--genfile`
create a prefilled service token file (default: `false`)
* `--help`, `-h`
show help info


#### **Output**
```
$ inigo create token test

service token created:
eyJ..1g

$ inigo create token --genfile test

service token created and prefilled service.token file
```