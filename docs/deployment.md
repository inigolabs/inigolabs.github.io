---
title: Deployment
has_children: true
nav_order: 4
layout: page
---

# Deployment
------------

Connecting Inigo to your GraphQL server is easy and requires no code changes or instrumentation from your end.  
To connect your server you'll first need to create a service and corresponding service token.  
A service represents a GraphQL endpoint running in your system. If you have multiple GraphQL endpoints, you can create a different service for each endpoint. Each service can run many instances or replicas as long as the GraphQL schema across the different instances are all the same.   
In case you have multiple environments such as dev, staging and production, use the service label attribute to distinguish between the different environments. 

Creating a service can be achieved in two way, using the cli or ui.

### [cli](/docs/cli.html) service creation
```
inigo create service <service_name>
inigo create token <service_name>
```
Replace `<service_name>` with the name you want to give this service endpoint.

### [ui](/docs/cli.html) service creation
Click the `Configure Services` button in the ui and follow the on screen instructions. 
<p align="center">
    <img src="/assets/images/configure_services.png" alt="Deployment" width="400"/>
</p>

Once you have your service created head over to your particular deployment to get up and running. If none of the available options match your usecase, let us know on <a href="https://slack.inigo.io" target="_blank">slack</a> or email support@inigo.io.  
We love to add more deployment options. 