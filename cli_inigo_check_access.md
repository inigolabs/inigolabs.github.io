---
title: "inigo check access"
parent: "inigo check"
has_children: false
nav_order: 2
---

## inigo check access
---
Check access prints out any errors or issues with the current access configuration for a given service.

```
inigo check access <service_name>
```

### Examples
```
> inigo check access starwars
demo/access/role/viewer  ok
demo/access/role/director  ok
demo/access/role/actor  ok
demo/access/role/producer  ok

> inigo check access starwars
demo/access/role/viewer
  access[viewer]: field "query.films.characters.invalid" not found in schema
demo/access/role/director  ok
demo/access/role/actor  ok
demo/access/role/producer  ok
```

### See also
- [inigo check schema](/cli_inigo_check_schema.html)
