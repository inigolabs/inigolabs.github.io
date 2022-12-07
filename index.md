---
title: Overview
has_children: false
layout: page
nav_order: 1
---

<link rel="shortcut icon" type="image/png" href="favicon.ico">

<p align="center">
  <img src="/assets/images/logo.svg" alt="Logo" width="250"/>
</p>


Welcome to <a href="https://inigo.io" target="_blank">Inigo</a> - the GraphQL Security and Management platform for your API.  
Inigo provides a server-agnostic management, security and observability solution layer for any GraphQL server.  

Inigo is a dynamic plug-and-play platform that works with any GraphQL server. The platform includes a suite of building blocks like schema-based access control, granular analytics, dynamic rate-limiting, an intuitive interface, and plenty more. Inigo is everything you need to speed up your GraphQL api development and adoption. Gain a unique and in-depth understanding of GraphQL usage through deep insights into the field level, query paths, and overall server health and performance. At Inigo we love GraphQL, our goal is to offer the absolute best developer and operational experience around GraphQL, so you can scale with confidence and efficiency.

Inigo works by running an agent together with your GraphQL server or gateway. The agent can run as middleware, sidecar, in docker or as a plugin to your gateway and requires no code changes to your server. Inigo supports many servers out of the box, integration is quick and easy. See the deployments section for all the currently available options. 
Using Inigo you can configure advanced schema based access control policies, rate limit different parts of your schema with ease, create security rules to protect your server against abuse, and much more. 

If you're here, you've probably signed up for an account at <a href="https://app.inigo.io" target="_blank">app.inigo.io</a> and are ready to start exploring how Inigo helps you manage and protect GraphQL APIs from malicious actors.


Inigo's powerful engine can enforce policies, alter and block incoming queries before they hit your GraphQL application servers.

<p align="center">
    <img src="/assets/images/deployment.png" alt="Deployment" width="400"/>
</p>

## Why protect your GraphQL API with Inigo
Unprotected GraphQL APIs can be vulnerable to a variety of security concerns, to list some:

1. Lack of Authentication and Authorization controls
2. Denial of Service vulnerabilities
3. Information Disclosure vulnerabilities
4. Hijacking and Forgery-based vulnerabilities

Inigo solves these complex security challenges by providing a comprehensive layer of enforcement, analytics and insights, all while decoupling the complex security logic from your application in a performant way that allows your business to focus on its highest priorities.

## Getting Started
The first step in the process is to explore the [Star Wars Demo Playground](docs/Tutorials/tutorials_starwars_playground.htm). The Star Wars API (also known as SWAPI) mimics the application that's protected by Inigo - in this case, your application. Once you get the hang of it, you can then apply your own [configuration](/docs/configuration.md). Configurations can be as strict as you want them to be and Inigo provides a comprehensive set of controls how tight the controls should be.

After exploring the demo playground and applying the sample configuration as provided by Inigo, you will get an idea how Inigo works. At which point you can then add your own service and apply your own server configuration.

Let's start:
1. [Starwars Demo Playground](/docs/Tutorials/tutorials_starwars_playground.html)
2. [Starwars Demo Configuration](/docs/Tutorials/tutorials_starwars_configuration.md)

For any questions, join our <a href="https://slack.inigo.io" target="_blank">Slack channel</a>.



