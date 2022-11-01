---
title: Kubernetes
parent: Deployment
has_children: false
nav_order: 3
layout: page
---

# Table of Contents
- [Table of Contents](#table-of-contents)
  - [Prerequisites](#prerequisites)
  - [Kubernetes](#kubernetes)


Prerequisites
-----

- A working Kubernetes instance with kubectl. If not, see the [Kubernetes documentation](https://kubernetes.io/docs/setup) for installation instructions.
- A working GraphQL Server instance.

Kubernetes
-----

  **Note:** this code snippet includes a starwars graphql example instance, make sure to replace with your own service.

  1. Create a `deployment.yaml` with the following content

  ``` yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: starwars
    spec:
      selector:
        matchLabels:
          app: starwars
      template:
        metadata:
          labels:
            app: starwars
        spec:
          containers:
            - name: starwars
              image: "inigohub/starwars:latest"
              imagePullPolicy: Always
              envFrom:
                - configMapRef:
                    name: starwars-configmap
            - name: sidecar
              image: "inigohub/sidecar:latest"
              imagePullPolicy: Always
              envFrom:
                - configMapRef:
                    name: starwars-sidecar-configmap
                - secretRef:
                    name: starwars-sidecar-token
    --- 
    apiVersion: v1
    kind: ConfigMap
    metadata:
      name: starwars
      labels:
        app: starwars
    data:
      #LOG_TYPE: "json"
      #LOG_LEVEL: "debug"
      SERVICE_LISTEN_PORT: "8888"
    ---
    apiVersion: v1
    kind: Secret
    metadata:
      name: starwars-sidecar-token
    stringData:
      INIGO_SERVICE_TOKEN: "YOUR_SERVICE_TOKEN_HERE"
    ---
    apiVersion: v1
    kind: ConfigMap
    metadata:
      name: starwars-sidecar
      labels:
        app: starwars
    data:
      #LOG_TYPE: "json"
      #LOG_LEVEL: "debug"
      INIGO_LISTEN_PORT: "80"
      INIGO_ENABLE: "true"
      INIGO_EGRESS_URL: http://localhost:8888/query
      INIGO_GRAPHQL_ROUTE: /query
      INIGO_GRAPHQL_PLAYGROUND_ROUTE: /playground
      INIGO_QUERYDATABATCH_MAX_TIME: 3s
      INIGO_QUERYDATABATCH_MAX_COUNT: "10"
    ---
    apiVersion: v1
    kind: Service
    metadata:
      name: starwars
      labels:
        app: starwars
    spec:
      type: NodePort
      ports:
        - port: 80
          targetPort: 80
      selector:
        app: starwars
  ```

  2. Make sure to replace `YOUR_SERVICE_TOKEN_HERE` with your own service token.

  3. Make sure to change starwars with your own service and its configurations.

  4. Make sure to correctly setup the `INIGO_EGRESS_URL` so that the ports are correctly configured.

  5. Apply the configuration using:
    ``` sh
      kubectl apply -f deployment.yaml
    ```