---
title: Python Django
parent: Deployment
has_children: false
nav_order: 3
layout: page
---

# Python Django Middleware

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
    'TOKEN': 'Your Inigo service token',
    'GRAPHENE_SCHEMA': 'app.schema.schema',
    'PATH': '/graphql',
    'JWT': 'authorization',
}
```

### Configuration options

#### __`DEBUG`__
**Optional. Default:** False

If not provided, Django DEBUG setting is used.

#### __`TOKEN`__
**Required.** Obtain a service token from [app.inigo.io](app.inigo.io)

#### __`GRAPHENE_SCHEMA`__
**Optional.** The path to graphene schema instance. If not provided, InigoMiddleware will try to pick it up from __`GRAPHENE.SCHEMA`__ settings.

#### __`SCHEMA_PATH`__
**Optional.** The path to graphql schema file.

#### __`PATH`__
**Optional. Default:** /graphql. 

Your graphql route path.

#### __`JWT`__
**Optional. Default:** authorization.

Name of your authorization header with jwt as a value. See **Authorization** for more details.

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
