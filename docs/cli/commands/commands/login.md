---
title: inigo login
parent: Command Line Interface (CLI)
has_children: false
nav_order: 2
layout: page
---

# inigo login
---

## Commands
- [inigo login](#inigo-login)
- [inigo login google](#inigo-login-google)
- [inigo login github](#inigo-login-github)


## Optional flags
* `help`, `h`
show help info

---

### ```inigo login```
#### **Description**
Authenticates to Inigo. Unless a particular identity provider is specified, the default authentication mode is via an email and password.

#### **Syntax**
```
inigo login
```

#### Optional flags
* `--help`, `-h`
show help info


#### **Output**
```
$ inigo login
username: demo@inigo.io
password: ************

login successful
```

---


### ```inigo login google```
#### **Description**
Authenticates to Inigo using Google. Authenticating using this option will open a browser window to complete the process.

#### **Syntax**
```
inigo login google
```

#### Optional flags
* `--help`, `-h`
show help info


#### **Output**
```
$ inigo login google

Opening in existing browser session.
...
login successful
```

---

### ```inigo login github```
#### **Description**
Authenticates to Inigo using GitHub. Authenticating using this option will open a browser window to complete the process.

#### **Syntax**
```
inigo login github
```

#### Optional flags
* `--help`, `-h`
show help info


#### **Output**
```
$ inigo login github

Opening in existing browser session.
...
login successful
```