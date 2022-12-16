---
title: Rust Apollo Router
parent: Deployment
has_children: false
nav_order: 7
layout: page
---

# Rust Apollo Router
--------------------

### Configuration
```yaml
plugins:
  inigo.middleware:
    token: "YOUR-INIGO-SERVICE-TOKEN"
```

### Plugin Registration
```rs
use anyhow::Result;
use apollo_router::register_plugin;
use inigo_rs::Middleware;

register_plugin!("inigo", "middleware", Middleware);

fn main() -> Result<()> {
    apollo_router::main()
}
```