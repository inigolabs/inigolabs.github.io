---
parent: Tutorials
has_children: false
nav_exclude: true
search_exclude: true
nav_order: 11
---

# Tutorial: How to set up simple access control for GraphQL operations

## Key information

> **TBD**: I need to print this out and go over it more carefully before calling it done, but all the steps are here, it's spell-checked and I just have to tech edit the details after some sleep.

Specific Indigo features that this tutorial covers include the following.

| Object | Data |
| --- | --- |
| Useful commands | `inigo apply configs/access.yml`|
| Useful URLs | `https://app.inigo.io` (developer dashboard)<br>`https://app.inigo.io/schema_view` (schema explorer) |
| Configuration files | `access.yml` (maps roles to access control configuration files)<br>`access/viewer.inigo` (configuration file for the `viewer` role) |  
| Configuration items | `config_files` | 
 
## Introduction

In this tutorial, you will:
* View the roles assigned to unauthenticated users and the access control configuration file for users with the `viewer` role.
* Add simple access control to the model in the configuration file, by adding an element to the schema exposed to users who are assigned the `viewer` role. 
* Learn the difference between edge-based and node-based access control.
* Explore the errors returned to a client when accessing nodes not available for their roles, and see how operations with and without access control errors are displayed on the Inigo dashboard.

Much of the power of GraphQL is in its ability to use a single API call to navigate through multiple types of (nodes) and the relationships between them (edges), to access or update data.

It's great because:
* Service designers don't have to anticipate all common use cases and data access patterns to design a service that is efficient and useful for their customers, and
* Client developers can use a single GraphQL operation to traverse a complex structure of data nodes and retrieve information that, without GraphQL, might have required 5 or 6 REST API calls.

However, this approach has a limitation: GraphQL out-of-the-box exposes your service's entire data model to every user of that service. A business in the real world may prefer to give different classes of users different levels of access. For example, you might offer two tiers of service:
* A free starter version of your service that provides a limited set of basic data, and
* A more advanced version that exposes additional data elements for a fee.

In a REST API, you could implement this by defining two endpoints that return different sets of data, and giving users access to one or both depending on their subscription level. To provide that functionality in a GraphQL API out-of-the-box, you need to develop your own solution, perhaps maintaining and running two separate services, each with its own schema and set of authorized users. Or perhaps you'd dig into your GraphQL's server code to implement a custom solution.

Inigo adds access control to GraphQL, allowing you to specify which schema nodes can be accessed by users with a particular role. When you do this:
* Users browsing a GraphQL schema see only the nodes to which they have access.
* Users executing a GraphQL operation can only reference nodes to which they have access. If the user requests nodes to which they do not have access, Inigo returns the graph of nodes they are allowed to access, and includes a list of the node paths for which access was denied.

A schema object may be referenced by more than one path through the GraphQL schema. Depending on your service, you may want to specify in Inigo:
* **Node-based** access control rules on that object that apply regardless of how it is referenced, or
* **Edge-based** access control rules that apply when the object is referenced through a specific path. 

This tutorial explores Inigo's edge-based access control. For information about node-based access control see [[HERE]].

It assumes that you are using the GraphQL example files created when you initialized the `demo` `starwars` service in the Getting Started tutorial, and the GraphQL `demo` `starwars` service in the GraphQL developer playground.

## Pre-requisites

To use this tutorial, you must have:

* The GraphQL command line utilities installed on your local system. For installation instructions see https://github.com/inigolabs/cli/blob/main/README.md
* A user ID and password that allows access to the GraphQL developer dashboard at https://dev.inigo.io and the developer playground at https://dev.inigo.io/starwars/playground. If you do not have access yet, go to https://dev.inigo.io and sign up!
* A `demo` service in your Inigo instance. This is created in the [Getting Started with Inigo tutorial](./tutorial_getting_started_with_inigo.md). If you haven't completed that tutorial yet, please do so before continuing with this one.

It is ideal if you are somewhat familiar with the starwars service schema often used as a GraphQL example. You can browse the schema using the [Schema View](https://dev.inigo.io/schema_view) option of the Inigo dashboard.

## Steps

### 1. Set up the unauthenticated user with the viewer role
1. Open the `starwars/access.yml` file in the examples project using a text editor.
2. Verify that the `spec:` section of the file has set up an unauthenticated `guest` user with the `viewer` role. Look for the following lines immediately after `spec:`
    ```
    unauthenticated_profile: guest  
    unauthenticated_roles:  
      - viewer  
    ```
    > **NOTE**: A profile can be assigned multiple roles, but to keep it simple we'll work with profile having a single role.
3. Within the `roles:` subsection of the file, ensure that the `viewer` role is associated with an Inigo config file as follows:
    ```
    - name: viewer  
      config_files:
        - access/viewer.inigo
    ```
    > **NOTE**: The access rules for a role may be contained in multiple `config_files`, but to keep it simple we'll work with with a single config file.
4. Save the file if you've made any changes to it.

### 2. View the access specification for the viewer role
> **TBD**: What are the contents of that file called? The access specification? The access rules? The access control definition? Something else?

1. Open the `access/viewer.inigo` file and view the initial access rules:
    ```
    query {
        login
        logout

        films
        people
    }

    type Film {
      title
      director
      characters
    }
    
    type Person {
      name
      hairColor
      ssn
    }
    ````
    These access control rules indicate that the viewer has access to the `login`, `logout`, `films`, and `people` nodes in the starwars service schema.
    
    Viewing the schema at `https://dev.inigo.io/schema_view`, you can see that `films` is an array of type `Film` and `people` is an array of type `Person`.
    
    When a node is an object (such as films) rather than a scalar value (such as title), you can specify the available contents of that object in two ways:
    * Edge-based: Specify access rules inline in { } within the query access rule.
    * Node-based: Specify access rules separately by object type.

    **Edge-based** access rules are most useful when multiple nodes at various paths share the same type, and you want different access rules to apply depending on the node path. For example, suppose your graph included both an `employees` node and a `teammates` node, and you wanted to expose more information about teammates than employees even though both are of type `Person`. We'll cover this in more detail later.

    **Node-based** access rules are useful when you want to apply the same access rules to nodes of that type, regardless of the path. For example, in the schema above, a user with the `viewer` role can access the `name`, `hairColor` and `ssn` values in all nodes of type `Person`.
2. Update the configuration on the Inigo Labs server to ensure these access rules apply to your service by running the following command line from the `starwars` directory:  
    ```
    inigo apply configs/*.yml
    ```

### 3. Run a test query in the Inigo playground
1. Open a browser window to the GraphQL playground at https://dev.inigo.io/starwars/playground
    > **NOTE:** Verify that the URL text box within the playground window contains `https://dev.inigo.io/starwars/query`. If it does not, paste that URL into the text box.
2. Copy the following query into the edit (left) pane:  
    ```graphql
    query ListFilmInfo {  
      films {  
        title
        characters {
          name
        }
      }
    }
    ```
3. Click the arrow icon between the panes, to execute that operation.  
4. Verify that you see a response like: 
    ```
    {
      "data": {
        "films": [
          {
            "title": "A New Hope",
            "characters": [
              {
                "name": "Luke Skywalker"
              },
              {
                "name": "C-3PO"
              },
              {
                "name": "R2-D2"
              },
              {
                "name": "Darth Vader"
              },
              {
                "name": "Leia Organa"
              },
              {
                "name": "Owen Lars"
              },
              {
                "name": "Beru Whitesun lars"
              },
              {
                "name": "R5-D4"
              },
              {
                "name": "Biggs Darklighter"
              },
              {
                "name": "Obi-Wan Kenobi"
              },
              {
                "name": "Wilhuff Tarkin"
              },
              {
                "name": "Chewbacca"
              },
              {
                "name": "Han Solo"
              },
              {
                "name": "Greedo"
              },
              {
                "name": "Jabba Desilijic Tiure"
              },
              {
                "name": "Wedge Antilles"
              },
              {
                "name": "Jek Tono Porkins"
              },
              {
                "name": "Raymus Antilles"
              }
            ]
          },
          [[ data for other films here... ]]
        ]
      },
      "extensions": {
        "inigo": {
          "status": "PASSED",
          "trace_id": "eed38d57-5093-447b-b859-e652d2928ca7"
        }
      }
    }
    ```

### 4. Update the access specification for the viewer role to include another schema element

1. Open the `access/viewer.inigo` file and update the access rules for the Film type to allow the `viewer` role to see the film `id`:
    ```
    query {
        login
        logout

        films
        people
    }

    type Film {
      title
      id
      director
      characters
    }
    
    type Person {
      name
      hairColor
      ssn
    }
    ````
2. Save the file.
3. Apply the configuration changes with the command:
    ```
    inigo apply configs/*.yml
    ```

### 5. Test that the id node is now accessible
1. Go back to the GraphQL playground browser window.
2. Copy the following text into the edit (left) pane:  
    ```graphql
    query ListFilmInfo {  
      films {  
        title
        id  
      }  
    }
    ```
3. Click the arrow icon between the panes, to execute that operation.  
4. Verify that you see a response like: 
    ```
    {
      "data": {
        "films": [
          {
            "title": "A New Hope",
            "id": 7846132940263424
          },
          {
            "title": "The Empire Strikes Back",
            "id": 7846132944457728
          },
          {
            "title": "Return of the Jedi",
            "id": 7846132944457729
          },
          {
            "title": "The Phantom Menace",
            "id": 7846132944457730
          },
          {
            "title": "Attack of the Clones",
            "id": 7846132944457731
          },
          {
            "title": "Revenge of the Sith",
            "id": 7846132944457732
          }
        ]
      },
      "extensions": {
        "inigo": {
          "status": "PASSED",
          "trace_id": "777b5bf8-cb12-4432-8f7d-3ddbc76b7d3b"
        }
      }
    }
    ```

  > **TBD**: Do we actually want to include those results, or should this step just say "Verify that the films' title and id are listed in the results" for brevity?

### 6. Access a node not allowed for the viewer role and observe the results

So far, we've only run queries that access schema elements available to the `viewer` role. In this step, we'll look at what happens when a query references a schema element for which it does not have permissions.

1. Open a browser window to the GraphQL playground at https://dev.inigo.io/starwars/playground
2. Copy the following text into the edit (left) pane:  
    ```graphql
    query ListFilmInfo {  
      films {  
        title
        id
        planets
      }  
    }
    ```
    > **NOTE:** The `planets` schema element in this query was not specified in the access control file for the `viewer` role, so it should not be accessible to our user.
    
3. Click the arrow icon between the panes, to execute that operation.  
4. The response you receive should have a `data` section, followed by an empty `extensions` section and an `errors` section indicating that this profile does not have access to the `films/planets` schema element: 
    ```graphql
    {
      "data": {
        "films": [
        {
          "title": "A New Hope",
          "id": 7846132940263424
        },
        {
          "title": "The Empire Strikes Back",
          "id": 7846132944457728
        },
        {
          "title": "Return of the Jedi",
          "id": 7846132944457729
        },
        {
          "title": "The Phantom Menace",
          "id": 7846132944457730
        },
        {
          "title": "Attack of the Clones",
          "id": 7846132944457731
        },
        {
          "title": "Revenge of the Sith",
          "id": 7846132944457732
        }
      ]
    },
    "extensions": {
      "inigo": {
        "status": "PASSED",
        "trace_id": "661462df-5ec1-4a07-8302-4b63dc533677"
      }
    },
    "errors": [
      {
        "message": "invalid access",
        "path": [
          "films",
          "planets"
        ]
      }
    ]
  }
    ```

### 3. See the blocked operation on the Indigo dashboard
1. Open the Inigo dashboard at https://dev.inigo.io and select the `Explore` option from the side menu.
2. See that the `Status` of the query is `Passed` because it did return some data, but it displays an `Invalid access` error.
3. Click the ID for that query to display a diagram of the requested query and the specific errors returned.

  > **TBD**: Can I include a screen shot of this, or is the UI still rev'ing so it would be obsolete too quickly?

You have now configured simple Inigo node-based access controls, and seen how they work.

## What's next
To configure edge-based access controls or configure access controls on the schema view to control the elements visible to a user when exploring your service's GraphQL schema, check out these tutorials:
* TBD
