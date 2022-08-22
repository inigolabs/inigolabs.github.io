---
title: Starwars Demo Configuration
parent: Tutorials
has_children: false
nav_order: 2
---

# Tutorial: Starwars Demo Configuration

## Download Access file

To be able to apply your own setting, download the [Starwars default configuration](/assets/files/starwars_default_config.zip).

## Apply changes

### security.yml:
1. Change require_operation_name from true to false
2. Change max_depth from 3 to 4
3. Change max_height from 9 to 14
4. Change max_directives from 5 to 30

### rate_limit.yml:
1. Change credits_per_minute to 50000

### access/viewer.yml
1. Add 'id' to filmes

## Install CLI

Get the Inigo CLI tool:
```console
brew tap inigolabs/homebrew-tap
```
Following by:
```console
brew install inigo_cli
```

## Login
Using the same credentials from [app.inigo.io](https://app.inigo.io)
```console
inigo login
```

## Apply Configuration 
Apply new configuration to the Starwars service
```console
inigo apply *.yml
```

## Replay Playground Queries
With the updated configuration, it's time to run the same queries again, see what the responses and visit [Inigo analytics console](https://app.inigo.io).


## What's next?
Contact us to add your own GraphQL server to Inigo.







