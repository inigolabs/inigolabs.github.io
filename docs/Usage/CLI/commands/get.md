---
title: inigo get
parent: Command Line Interface (CLI)
grand_parent: Usage
has_children: false
nav_order: 5
layout: page
---

# inigo get
---

## Commands
- [inigo get service](#inigo-get-service)
- [inigo get instance](#inigo-get-instance)
- [inigo get access](#inigo-get-access)

## Optional flags
* `help`, `h`
show help info

---

### ```inigo get service```
#### **Description**
Retrieves information about services.

#### **Syntax**
```
inigo get service
inigo get service [service_name]
inigo get service [service_name][:label_name]
inigo get service --label [:label_name] [service_name]
```

#### Optional flags
* `--label <value>`
retrieves information by a service label name
* `--json`
output in json format (default: `false`)
* `--help`, `-h`
show help info


#### **Output**
```
$ inigo get service

NAME  LABEL     INSTANCES  STATUS
----  -----     ---------  ------
demo  starwars  0          1  Running
demo  remote    0          1  Running
test            0          1  Running

$ inigo get service demo:starwars

Configurations:
  user role path: jwt.user_roles
  user profile path: jwt.user_profile
  user id path: jwt.user_name
  traceId path:
  schema polling interval: 5m0s
  profile polling interval: 2s

$ inigo get service --label starwars demo

Configurations:
  user role path: jwt.user_roles
  user profile path: jwt.user_profile
  user id path: jwt.user_name
  traceId path:
  schema polling interval: 5m0s
  profile polling interval: 2s


$ inigo get service --json
  --snip--
  [
    {
        "Id": 3210674112131072,
        "Name": "demo",
        "Label": "starwars",
        "Config": {
        "Service": {
            "PollingIntervalProfile": 2
        }
        },
        "Instances": [
        {
            "Id": 3210677102657536,
            "LastUpdated": "2022-09-16T16:22:48.448629Z",
            "Total": 11,
            "Error": 0,
            "Blocked": 2,
            "Modified": 0
        }
        ]
    }
  --snip--
  ]
```

---

### ```inigo get instance```
#### **Description**
Retrieves information about sidecar instances.

#### **Syntax**
```
inigo get instance
```

#### Optional flags
* `--json`
output in json format (default: `false`)
* `--help`, `-h`
show help info


#### **Output**
```
$ inigo get instance

ID  SERVICE  TOTAL  BLOCKED  MODIFIED  ERROR  UPDATED
--  -------  -----  -------  --------  -----  -------

$ inigo get instance --json

  --snip--
  [
    {
        "Id": 3210674112131072,
        "Name": "demo",
        "Label": "starwars",
        "Config": {
        "Service": {
            "PollingIntervalProfile": 2
        }
        },
        "Instances": [
        {
            "Id": 3210677102657536,
            "LastUpdated": "2022-09-16T16:22:48.448629Z",
            "Total": 11,
            "Error": 0,
            "Blocked": 2,
            "Modified": 0
        }
        ]
    },
  --snip--
  ]
```

---

### ```inigo get access```
#### **Description**
Retrieves access profile information for a given service

#### **Syntax**
```
inigo get access [service_name]:[:label_name] [role_name]
```

#### Optional flags
* `--full`
display full access, including fields with errors (default: `false`)
* `--label`
retrieves access profile by a service label name
* `--help`, `-h`
show help info


#### **Output**
```
$ inigo get access demo:starwars

viewer :
query {
	films {
		characters {
			appearedIn: Film
			name
		}
		director
		title
	}
	login
	logout
	people: Person
}

type Film {
	characters: Person
	director
	title
}

type Person {
	birthYear
	height
	name
	ssn
}
--snip--

$ inigo get access demo:starwars actor

actor :
query {
	login
	logout
	version {
		commit
		date
		version
	}
}

mutation {
	userAdd
	userRemove
}
```