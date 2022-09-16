---
title: @access directive
has_children: false
nav_exclude: true
search_exclude: true
nav_order: 2
---

# Tutorial: How to set up access control using `@access` directive

## Prerequisites:
1. Create valid access role that later will be extended with the use of `@access` directive:
```superuser.inigo
query {
	films {
        director
        title
    }
}
```

2. Add definition of `@access` directive to your service schema:
```schema.graphql
directive @access(
	role: [String] = ["allowed role"]
	depth: Int
) on FIELD_DEFINITION
```

3. Assign `@access` directive for the field to which you want to grant access:
```schema.graphql
type Query {
    ...
	planets: [Planet!]! @access(role:["superuser"])
}
```

4. Finally, add configuration schema to your service config:
```service.yml
kind: Service
spec:
  ...
  schema_files:
    - ../../go/starwars/graphql/schema.graphql
```

5. After applying service config the of resulting access role will look like this:
```superuser :
query {
	films {
		director
		title
	}
	planets {
		*
	}
}
```
---

## Important notes:
* A valid role has to be created before using it with `@access` directive
* Use `depth` parameter for the directive `@access` to restrict access to a certain depth. 
If depth parameter is omitted then the access will be provided for the whole depth of underlying query.
* After updating service schema always re-apply your service config for changes to take place.