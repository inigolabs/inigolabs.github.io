---
title: inigo login
parent: CLI
has_children: false
nav_order: 2
---

## inigo login
---
```
inigo login
```
Authenticate and login to Inigo.
The default authentication mode is via email and password.  
Google and GitHub sso authentications are also available.

### Commands
- inigo login  
&nbsp;&nbsp;&nbsp;Enter the username and password when prompted.
- inigo login google    
&nbsp;&nbsp;&nbsp;Login using your google account. A web browser window will open to complete the sign in using google.

- inigo login github  
&nbsp;&nbsp;&nbsp;Login using your github account. A web browser window will open to complete the sign in using github.

### Examples
```
> inigo login
username: bob@graphql.com
password: ****
login successful

> inigo login google
login successful

> inigo login github
login successful
```

### See also
- [inigo logout](/cli_inigo_logout.html)
