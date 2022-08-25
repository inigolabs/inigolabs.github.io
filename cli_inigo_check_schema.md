---
title: "inigo check schema"
parent: "inigo check"
has_children: false
nav_order: 1
---

## inigo check schema
---
Check for breaking schema changes.
The check schema command will check wether the supplied schema has any breaking changes. The command uses analytics data from the last 30 days to see if any removed or updated fields will result in broken clients. 
```
inigo check schema <service_key> <schema_files>
```

### Example
```
> inigo check schema starwars schema/starwars.graphql
TODO - sample output here
```

### See also
- [inigo check access](/cli_inigo_check_access.html)
