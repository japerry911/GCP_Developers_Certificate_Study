# Section 5 - Managed Services in Google Cloud Platform

### Introduction

- IaaS (Infrastructure as a Service)
- PaaS (Platform as a Service)
- FaaS (Function as a Service)
- CaaS (Container as a Service)
- Serverless

### IaaS and PaaS

- IaaS
  - use only infrastructure from cloud provider
    - example
      - using VM to deploy your applications or databases
  - you are responsible for
    - applciation code and runtime
    - configuring load balancing
    - auto scaling
    - OS upgrades and patches
    - availability
    - etc...
- PaaS
  - uses a platform provided by cloud
  - cloud provider is responsible for
    - OS, upgrades & patches
    - application runtime
    - auto scaling, availability, and load balancing
  - you are responsible for
    - configuration of application and services
    - application code (if needed)
  - varieties
    - CaaS - containers instea of apps
    - FaaS - functions instead of apps
    - databases

### Containers

- microservices
  - build small focused microservices
  - flexibility to innovate and build applications in different programming languages
  - con: deployments are more complex
    - how can we have one way of deploying microservices
      - **containers**
- docker
  - create docker images for each microservice
  - image has all needs of a microservice
  - runs the same way on any infrastructure
  - advantages
    - container are lightweight
      - do not have a Guest OS, when compared to VMs
    - isolation for containers
    - cloud neutral
- container orchestration
  - kubernetes
  - typical features
    - auto scaling
      - scale containers based on demand
    - service discovery
      - help microservices find one another
    - load balancer
      - distribute load among multiple instances of a microservice
    - self healing
      - do health checks and replace failing instances
    - zero downtime deployments
      - release new versions without downtime

### Serverless

- don't need to worry about servers and can focus on your code
  - don't worry about infastructure (zero visibility into infrastructure)
    - flexibile scaling and automated high availability
  - pay for use
    - when you pay, you pay for requests and not servers
- FaaS

### GCP Managed Services for Compute

- Compute Engine
  - high-performance and general purpose VMs that scale globally
  - IaaS
- Google Kubernetes Engine
  - orchestrate containerized microservices on Kubernetes, needs advanced cluster configuration and monitoring
  - CaaS
- App Engine
  - build highly scalable applications on a fully managed platform using open and familiar languages and tools
  - PaaS (can also be: CaaS, Serverless)
- Cloud Functions
  - build event driven applications using simple, single-purpose functions
  - FaaS, serverless
- Cloud Run
  - develop and deploy highly scalable containerized applications. Does not need a cluster
  - CaaS (serverless)
