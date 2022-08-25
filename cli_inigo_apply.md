---
title: inigo apply
parent: CLI
has_children: false
nav_order: 4
---

## inigo apply
---
Apply inigo configurations to a service.  
The command prints out status for any configuration that has changed, possible statuses are [created, updated, removed].  
Configuration yaml files can be passed in individually or using a glob to apply multiple configuration files at once.  
```
inigo apply <yaml_config_filenames>  
```

### Examples
```
> inigo apply configs/service.yml
starwars/service created

> inigo apply configs/security.yml
starwars/security updated
starwars/security/profiles/viewer created

> inigo apply configs/access.yml
starwars/access created
starwars/access/roles/viewer created

> inigo apply configs/rate_limit.yml

> inigo apply configs/*.yml
starwars/service updated
starwars/access/profiles/guest created
starwars/access/roles/viewer updated
starwars/security/profiles/anonymous removed
starwars/rate_limit/profiles/admin updated
starwars/rate_limit/profiles/user updated
```

### Options
`--wait`  
&nbsp;&nbsp;&nbsp;wait for configuration to be applied to service instance 

`--wait-for <number_of_instances>`  
&nbsp;&nbsp;&nbsp;wait for particular number of instances to become updated (default: 0)

`--label`  
&nbsp;&nbsp;&nbsp;apply configuration to service with a particular label

`--timeout <seconds>`  
&nbsp;&nbsp;&nbsp;if provided cancels the apply wait when it exceeds the timeout value


### See also
- [inigo get](/cli_inigo_get.html)
- [inigo create](/cli_inigo_create.html)




