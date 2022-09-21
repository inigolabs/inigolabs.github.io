---
title: Star Wars Demo Playground
parent: Tutorials
has_children: false
nav_order: 1
---

# Tutorial: Star Wars Demo Configuration

## What is it?

The Star Wars Demo Playground comes prefilled with sample queries to give you the sense of how Inigo can help to protect your GraphQL server against malicious GraphQL operations.

## Access Playground

1. Log into your account at <a href="https://app.inigo.io" target="_blank">app.inigo.io</a> with your credentials
2. Click the **Playground** button located at the top left corner as shown below.

![Playground Access](/assets/images/playground_access.png)

## Prefilled Queries to Test
The Playground will include prefilled queries (in the form of playground tabs) - they are used to give you quick access to various queries that make use of GraphQL's declarative query language, all while providing you with the opportunity to observe how Inigo can handle these queries.
![image](https://user-images.githubusercontent.com/9330805/185870446-b3ea057c-5a10-4c7b-8ad8-d3a5ce5e045b.png)

Below you will find information about each query.

### missingOperationsName
Inigo can enforce that all queries must have an operation name. When clients attempt a query without an operation name, Inigo can block this query from being processed by your application.

```
query {
  films {
    title
  }
}
```

### maxDepth
Inigo can protect your GraphQL API by enforcing a limit on the query's depth. By default, A maximum depth limit was set to `3`. If a client constructs a more complex query, Inigo will be able to detect and block it immediately before the query exhausts your server's resources.

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
Inigo can protect your GraphQL API by enforcing a maximum height limit. In the builtin policy, a maximum query height is set to `9`. Any query that exceeds this threshold will be blocked with Inigo's policy enforcement.
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
Clients can specify query directives and by default there is no limitation on how many can be provided. The number of maximum directives is set to `5`. Inigo will block any query that exceeds the set amount.

```
query maxDirectives {
  films @a@aa@aaa@aaaa@a@aa@aaa@aaaa@a@aa@aaa@aaaa@a@aa@aaa@aaaa@a@aa@aaa@aaaa@a@aa@aaa@aaaa@a@aa@aaa@aaaa {
    title
    characters {
      name
    }
  }
}
```

### invalidAccess
Inigo can provide an authorization layer to your GraphQL API, providing a decoupled solution from your application. When a client is anonymously attempting to access a certain field, Inigo will block the violating client.

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
Most GraphQL APIs security libraries provide stateless rate limiting controls. Inigo's stateful rate limiting mechanism allows tracking client usage and enforcing limitations across sessions. When a client exceeds their credit allowance, Inigo can automatically block the query. Running the `hitMaxCredits` query several times will contribute to the client's credit usage. Once the client hits the limit, no further querying is allowed.

```
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

## Other Security Features
Inigo provides additional defenses against malicious queries. These 5 samples are there to give you insight into some of its anti-abuse capabilities.

## Violation Monitoring through Intelligent Analytics
Visiting the <a href="https://app.inigo.io" target="_blank">Inigo Analytics Console</a> is where GraphQL usage can be explored, and potential abuse through GraphQL queries can be investigated.

## What's Next
Let's walk through the steps to apply our own configurations to the Star Wars server - [Star Wars Demo Configuration](/tutorials_starwars_configuration.html).
