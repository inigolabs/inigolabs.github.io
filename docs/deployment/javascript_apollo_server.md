---
title: JavaScript Apollo Server
parent: Deployment
has_children: false
nav_order: 2
layout: page
---

# Apollo Server Middleware
--------------------------

### Installation

1. Install the `inigo.js` middleware package
   ```sh
   npm install inigo.js
   ```
2. Install your platform specific library:
    ```sh
    npm install inigo-linux-amd64
    ```
    Available libraries:
    - inigo-linux-amd64
    - inigo-linux-arm64
    - inigo-alpine-amd64
    - inigo-alpine-arm64
    - inigo-darwin-amd64
    - inigo-darwin-arm64
    - inigo-windows-amd64

### Configuration
1. Import `InigoPlugin` & `InigoConfig` from `inigo.js` module
    ```js
    import { InigoPlugin, InigoConfig } from 'inigo.js';
    ```

    - ### For predefined GraphQL schema definitions
      - Create an inigo config object
        ```js
        const inigoCfg = new InigoConfig({
            Token: "YOUR-INIGO-SERVICE-TOKEN", // Input token generated using inigo cli or web panel
            Schema: typeDefs // String based SDL format GraphQL Schema
        });
        ```

    - ### For runtime-generated GraphQL schema definitions
      [GraphQL.js](https://www.npmjs.com/package/graphql) utilities can be utilized for conversion.

      1. Install the `graphql` package
          ```sh
          npm install graphql
          ```

      2. Import `printSchema` from `graphql` package
          ```js
          import { printSchema } from 'graphql';
          ```

      3. Create an inigo config object
          ```js
          const inigoCfg = new InigoConfig({
              Token: "YOUR-INIGO-SERVICE-TOKEN", // Input token generated using inigo cli or web panel
              Schema: printSchema(typeDefs) // Convert GraphQLSchema object to SDL format
          });
          ```

2. Plug in the middleware by adding the following to `plugins` within `ApolloServer`
    ```js
    InigoPlugin(inigoCfg)
    ```

    Result:
    ```js
    const server = new ApolloServer({
        typeDefs,
        resolvers,
        introspection: true,
        plugins: [
            InigoPlugin(inigoCfg) // <---
        ]
    });
    ```

3. Your final configuration should look like the following example
    ```js
    import { ApolloServer } from 'apollo-server';
    import { InigoPlugin, InigoConfig } from 'inigo.js'; // <---

    const typeDefs = `
        type Query {
            hello: String
        }
    `;

    const resolvers = {
        Query: {
            hello: () => 'world',
        },
    };

    const inigoCfg = new InigoConfig({  // <---
        Token: "eyJhbGc..",             // <---
        Schema: typeDefs                // <---
    });                                 // <---

    const server = new ApolloServer({
        typeDefs,
        resolvers,
        introspection: true,
        plugins: [                      // <---
            InigoPlugin(inigoCfg)       // <---
        ]                               // <---
    });

    server.listen().then(({ url }) => {
        console.log(`???? Server ready at ${url}`);
    });
    ```

### Passing Authentication using JWT header
  1. Configure and apply your `service.yml`
  ```yaml
  kind: Service
  name: starwars
  spec:
    path_user_id: jwt.user_name
    path_user_profile: jwt.user_profile
    path_user_role: jwt.user_roles
  ```

  2. Configure `ApolloServer` to pass in an `inigo` object within context containing the `jwt` from the request headers. 
  > Note: `jwt` is always prioritized when found with `ctx` or other.
  ```js
  const server = new ApolloServer({
    typeDefs,
    resolvers,
    introspection: true,
    plugins: [
      InigoPlugin(inigoCfg)
    ],
    context: async ({ req }) => {
      return { 
        inigo: {
          jwt: req.headers.authorization ?? ""
        }
      }
    }
  );
  ```

### Passing Authentication using Context

  1. Configure and apply your `service.yml`
  ```yaml
  kind: Service
  name: starwars
  spec:
    path_user_id: ctx.user_name
    path_user_profile: ctx.user_profile
    path_user_role: ctx.user_roles
  ```

  2. Configure `ApolloServer` to pass in an `inigo` object containing context.
  > Note: `jwt` is always prioritized when found with `ctx` or other.

  > Note: It's important to have object names identical to what was referenced in the service.yml
  ```js
  const server = new ApolloServer({
    typeDefs,
    resolvers,
    introspection: true,
    plugins: [
      InigoPlugin(inigoCfg)
    ],
    context: async ({ req }) => {
      return { 
        inigo: {
          ctx: {
            user_name: "yoda", 
            user_profile: "admin",
            user_roles: [ "producer", "director", "actor", "viewer" ],
          }
        }
      }
    }
  );
  ```
