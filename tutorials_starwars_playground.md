---
title: Starwars Demo Playground
parent: Tutorials
has_children: false
nav_order: 1
---

# Tutorial: Starwars Demo Configuration

## What is it?

The Starward Demo Playground comes prefilled with sample queries to get a feeling of how Inigo can help to protect your GraphQL server.   


## Access Playground

1. Log in to your account at [app.inigo.io](https://app.inigo.io)
2. Click and access the Playground

![Playground Access](/assets/images/playground_access.png)

## Prefilled Queries to Test

Starting with some basic example queries to see how Inigo secure the Starwars server
![image](https://user-images.githubusercontent.com/9330805/185870446-b3ea057c-5a10-4c7b-8ad8-d3a5ce5e045b.png)


### missingOperationsName
By default, all queries must have an operation name. See what happens when they don't.

```
query {
  films {
    title
  }
}
```

### maxDepth
By default, max depth was defined as 3. See what happens if a query passes that.

```
query maxDepth {
  films {
    title
    characters {
      appearedIn {
        title
      }
    }
  }
}
```

### maxHeight
By default, max height was defined as 9. See what happens if a query passes that.

```
query maxHeight {
  films {
    director
    title
    characters {
       name
    }
  }

  people {
    name
    birthYear
    height
    ssn
  }
}
```

### maxDirectives
By default, max directives were defined as 5. See what happens if a query passes that.

```
query maxDirectives {
  films @a@aa@aaa@aaaa@a@aa@aaa@aaaa@a@aa@aaa@aaaa@a@aa@aaa@aaaa@a@aa@aaa@aaaa@a@aa@aaa@aaaa@a@aa@aaa@aaaa{
    title
    characters {
      name
    }
  }
}
```

### invalidAccess
See what happens anonymous users try to access fields they don't have access to.

```
query invalidAccess {
  films {
    id
    director
    title
  }
}
```

### hitMaxCredits
Rate limiting is defined by the number of returned objects per minute. See what happens if a query passes that.

```
# Run 5-10 times
query hitMaxCredits {
  films {
    title
    characters {
      name
      birthYear
      height
    }
  }
}
```

## What's Next

Let's walk through the steps to apply our own configurations to the Starwars server - [Starwars Demo Configuration](/tutorials_starwars_configuration.html).
