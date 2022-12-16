---
title: Standalone Agent
parent: Deployment
has_children: false
nav_order: 1
layout: page
---

# Standalone Agent
------------------

### Installation

Download the inigo agent binary for your platform from the [artifacts](https://github.com/inigolabs/artifacts/releases) page. Set correct the binary permissions with `chmod +x` in order to execute the agent. 

### Basic Configuration

Configuring the agent can be done using a yaml config file names `config.yml` or environment variables.  
You can use both configuration methods together. For instance you should not store your token in your repository, you can use the environment variable for the token and the `config.yml` for the other coniguration knobs.  
In case a configuration knob is present in both the yaml and environment, the environment variable will take higher precedence. 

#### yaml 
  ``` yaml
  EgressURL: https://localhost:4000/query
  ServiceToken: "YOUR-INIGO-SERVICE-TOKEN"
  ```

#### environment variable
  ```bash
  INIGO_EGRESS_URL = "https://localhost:4000/query"
  INIGO_SERVICE_TOKEN = "YOUR-INIGO-SERVICE-TOKEN"
  ```

### All Configurations
You can customize certain functionalities of the agent using the configuration yaml file or via environment variables.  
The table below contains a detailed description of all the available toggles and buttons of the agent.

When you need to override any runtime defaults, you will export your environment variable and set it to the correct value. For example: `export INIGO_LOG_LEVEL=debug`.

| Environment Variable | YAML Config | Type | Required | Description |
| ---  | :---: | --- | --- | --- | --- |
| `INIGO_EGRESS_URL` | `EgressURL` | `string` | Yes | URL of the proxied application (GraphQL Endpoint) |
| `INIGO_SERVICE_TOKEN` | `ServiceToken` | `string` | Yes | Service token obtained from Inigo |
| `INIGO_LOG_LEVEL` | `LogLevel` | `string` | No<br>default: `info`| Logging level |
| `INIGO_LOG_TYPE` | `LogType` | `string` | No<br>default: `text`| Logging format [`json`, `text`]|
| `INIGO_LISTEN_PORT` | `ListenPort` | `integer` | No<br>default: `80`| TCP port to bind the agent to |
