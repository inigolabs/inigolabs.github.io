---
title: Python Django
parent: Deployment
has_children: false
nav_order: 3
layout: page
---

# Python Django Middleware
--------------------------

### Installation

```shell
pip install inigo-py
```

### Django Settings

```python
MIDDLEWARE = [
    ...
    'inigo_py.DjangoMiddleware',
]

INIGO = {
    'DEBUG': False,
    'TOKEN': 'YOUR-INIGO-SERVICE-TOKEN',
    'GRAPHENE_SCHEMA': 'app.schema.schema',
    'PATH': '/graphql',
    'JWT': 'authorization',
}
```

### Configuration options

| Name | Type | Required | Description |
| --- | --- | --- | --- |
| `TOKEN` | `string` | Yes | Service token |
| `GRAPHENE_SCHEMA` | `string` | No<br>default:`GRAPHENE.SCHEMA` | Path to graphene schema instance |
| `SCHEMA_PATH` | `string` | No | Path to GraphQL schema file |
| `PATH` | `string` | No<br>default:`/graphql` | Path to GraphQL schema file |
| `JWT` | `bool` | No<br>default: `Authorization` | JWT authorization header key name |
| `DEBUG` | `bool` | No<br>default: `False` | Enable debug mode |

---

### Authentication 

#### Passing Authentication using JWT header
1. Configure and apply your `service.yml`
  ```yaml
  kind: Service
  name: <service_name>
  spec:
    path_user_id: jwt.user_name
    path_user_profile: jwt.user_profile
    path_user_role: jwt.user_roles
  ```

2. Provide name of the header into Djang configuration
```python
INIGO = {
    'JWT': 'authorization'
}
```

> NOTE. Payload of the decoded jwt should match with the provided above configuration.

#### Passing Authentication using Context

1. Configure and apply your `service.yml`
  ```yaml
  kind: Service
  name: <service_name>
  spec:
    path_user_id: ctx.user_name
    path_user_profile: ctx.user_profile
    path_user_role: ctx.user_roles
  ```

2. Configure `Django` to pass in an `InigoContext` object.

  ```python
from inigo_py import InigoContext

# define middleware to pass authentication via ctx
def auth(get_response):
    def middleware(request):

        request.inigo = InigoContext()
        request.inigo.auth = {
            'user_name': 'me',
            'user_profile': 'guest',
            'user_roles': [],
        }

        return get_response(request)

    return middleware

# add middleware to Django settings. Make sure to add it before `inigo_py.DjangoMiddleware` as it's providing info required for correct request processing.
MIDDLEWARE = [
    ...
    'middleware.auth',
    'inigo_py.DjangoMiddleware',
]
  ```

> Note: if auth object provided on request, `JWT` header is not used
