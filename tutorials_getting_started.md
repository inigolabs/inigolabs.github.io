---
title:
parent:
has_children: false
nav_exclude: true
search_exclude: true
nav_order: 10
---

# Tutorial: Getting started with Inigo

## Key information

Specific Inigo features that this tutorial covers include the following.

| Object | Data |
| --- | --- |
| Useful commands | `inigo create service --init --label starwars demo`<br>`inigo get services`<br>`inigo apply configs/service.yml`|
| Configuration files | `service.yml` (contains operation name) |
| Configuration items | `require_operation_name` |

## Introduction

Welcome to the Inigo platform!

If you're here, you've probably signed up for an account at http://app.inigo.io, and are ready to start exploring how Inigo helps you manage GraphQL APIs.

In this tutorial, you will:
* Create an Inigo sample service based on the well-known starwars GraphQL sample service,
* Check the status of all of your Inigo services, and
* Configure the sample service to require named operations.

Adding a new service to your Inigo instance creates default configuration files on your machine and tells the Inigo server to initialize the new service.

Requiring named GraphQL operations enables you to best utilize the power of Inigo's API management dashboard, which displays a log of the operations executed against your GraphQL API.

Log entries on the dashboard include the operation name, if provided, so that you can easily determine the log data relevant to a a particular operation. Information you can see includes how often each specific query or mutation is being run, by whom, how many resources it uses, and whether the operation was allowed or blocked by Inigo access controls. Analyzing the dashboard's data allows you to detect if certain operations are executed more often at certain times of the day, providing opportunities for tuning cloud service resources.

With GraphQL out-of-the-box, operation names are optional. To help your organization collect the most useful API usage data, Inigo enables you to require all queries and mutations to be named. We strongly recommend that you configure each new GraphQL API to require named operations, as described in this tutorial.

## Pre-requisites

To use this tutorial, you must have:

* The GraphQL command line utilities installed on your local system. For installation instructions see [Installing the Inigo CLI tools](../guides/installing-inigo-cli-tools.md).
* A user ID and password that allows access to the GraphQL developer dashboard at https://app.inigo.io and the developer playground at https://dev.inigo.io/starwars/playground. If you do not have access yet, go to https://app.inigo.io and sign up!

## Steps
### 1. Initialize a new GraphQL API on Inigo
1. Navigate to the folder in which you want to store the Inigo configuration files.
2. Run the following from the command line to create a `starwars` folder containing default configuration files:
    ````
    inigo create service --init --label starwars demo
    ````
    > **TBD**: The version of the inigo command I have (Linux, if it matters), 0.12.0, does not have the --init option and brew says it's the latest version, so I could not test this command.

    If the command completed without errors, your new Inigo service should now exist. If a `demo` service was already defined for your Inigo instance, the command will display the error:
    ````
    : mutation.serviceAdd: service 'demo2:starwars2' already exists
    ````

    > **TBD**: Didn't know whether to recommend that they delete the existing demo service and re-run the create, or create a service under a different name. The latter may be confusing when going through future tutorials.  IMHO, it is realistic to assume that a new user may do this tutorial more than once, weeks or months apart depending on their schedule for exploring Inigo -- if you think this is a bad assumption, let me know!

### 2. Display the list of GraphQL API services on Inigo
1. Run the following from the command line to view the status of all services and verify the name (`demo`) and label (`starwars`) of your demo service:
    ````
    inigo get services
    ````
    This should show the service you just created above:
    ````
    NAME      LABEL      PROFILES  INSTANCES  STATUS
    ----      -----      --------  ---------  ------
    demo      starwars   0         1          Running
    ````

### 3. Configure the new service to require named operations
1. Open the `starwars/configs/service.yml` file in the examples project using a text editor.
2. Find the `guest` profile section by searching for:
``  - name: guest``
    > **NOTE**: This tutorial configures only the `guest` profile. For most real-world use cases, you would configure this setting for every profile in `service.yml`.
3. Within that profile section, find the line beginning with:
``    require_operation_name: ``
4. If the value of this setting is already `true`, your configuration is already set to require named operations. Go to step 5 to ensure that the configuration has been pushed up to Inigo. Otherwise, if the value is `false`, change the line to read:
``    require_operation_name: true``
5. Save the file.
6. Update the configuration on the Inigo Labs server, by running the following command line from the `starwars` directory:
    ```
    inigo apply configs/service.yml
    ```

### 4. Verify the change
1. Open a browser window to the GraphQL playground at https://app.inigo.io/starwars/playground
    > **NOTE:** Verify that the URL text box within the playground window contains `https://app.inigo.io/starwars/query`. If it does not, paste that URL into the text box.
2. Copy the following text that defines an unnamed query into the edit (left) pane:
    ```graphql
    query {
      films {
        title
      }
    }
    ```
3. Click the arrow icon between the panes, to execute that operation.
4. Verify that you see a response like:
    ```graphql
    {
      "data": null,
          "extensions": {},
          "errors": [
            {
              "message": "nameless operations are not  allowed"
            }
          ]
      }
    ```

      > **NOTE:** If you see a list of films, named operations are not yet required. Go back through [Steps](#steps) 1-6 of the tutorial and verify that you've performed all the steps.

5. Return to the edit window and replace the line:
    ```
    query {
    ```
    with
    ```
    query ListFilms {
    ```
6. Click the arrow icon between the panes, to execute the revised query.
7. Verify that you see a response like:

    ```
    {
        "data": {
          "films": [
            {
                "title": "A New Hope"
            },
            {
                "title": "The Empire Strikes Back"
            },
            {
                "title": "Return of the Jedi"
            },
            {
                "title": "The Phantom Menace"
            },
            {
                "title": "Attack of the Clones"
            },
            {
                "title": "Revenge of the Sith"
            }
          ]
        },
        "extensions": {}
    }
    ```

Congratulations! Your Inigo GraphQL server is now set up to require named operations for all users assigned the guest profile.

## What's next
To learn more about Inigo, check out our other tutorials:
* TBD list
