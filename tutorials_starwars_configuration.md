---
title: Starwars Demo Configuration
parent: Tutorials
has_children: false
nav_order: 2
---

# Tutorial: Starwars Demo Configuration

## Download Access files

To be able to apply your own setting, download the [Star Wars default configuration](/assets/files/starwars_default_config.zip).

Next, let's start experimenting with some of Inigo's security enforcement capabilities by modifying and applying the following changes.

## Configuration Changes

### security.yml:
1. Change `require_operation_name` from `true` to `false`
2. Change `max_depth` from `3` to `4`
3. Change `max_height` from `9` to `14`
4. Change `max_directives` from `5` to `30`

### rate_limit.yml:
1. Change `credits_per_minute` to `50000`

### access/viewer.inigo
1. Remove the `title` field from `films`

## Install CLI

Get the Inigo CLI tool:
```shell
brew tap inigolabs/homebrew-tap
brew install inigo_cli
```
Other installation [options](/cli.html])

## Login
Using the same credentials from <a href="https://app.inigo.io" target="_blank">app.inigo.io</a>
```shell
inigo login
```

## Apply Configuration
Apply new configuration to the Starwars service
```shell
inigo apply *.yml
```

## Replay Playground Queries
With the updated configuration, it's time to run the same queries again, see what the responses and visit <a href="https://app.inigo.io" target="_blank">Inigo Analytics Console</a>.


## What's next?
<a href="https://slack.inigo.io" target="_blank">Contact us</a> to add your own GraphQL server to Inigo.


