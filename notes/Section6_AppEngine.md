# Getting Started with Google App Engine

### Introduction

- simplest way to deploy and scale application in GCP
  - provides end-to-end application management
- supports a variety of languages using pre-configured runtimes
  - can also use a custom runtime and write code in any language
  - connect to a variety of GCS services easily
- no usage charges - pay for resources provisioned
- features
  - automatic load balancing & auto scaling
  - managed platform updates and application health monitoring
  - application versioning
  - traffic splitting
- versus compute engine
  - compute engine is infrastructure as a service
    - lots of flexibility, which creates a lot of responsibility
      - need to choose hardware, software, image, etc...
  - application is platform as a service
    - serverless
    - less responsibility, which results in less flexibility

### App Engine Environments

- environments
  - standard - applications run in language specific sandboxes
    - complete isolation from OS/disk/other apps
    - v1 (old versions)
      - restrictions for Python and PHP
    - v2 (newer versions)
      - no restrictions on language extensions
  - flexible - application instances run within Docker containers
    - make use of compute enigne virtual machines
    - support any runtime
    - provides access to background processes and local disks
- comparison
  -

### Component Hierarchy

![App Engine Hierarchy](./assets/app_engine_hiearchy.png 'App Engine Hiearchy')

- application - one app per project
- service(s) - multiple microservices or app components
  - example - frontend and backend would be separate services
  - each service can have different settings
  - earlier called modules
- version(s) - each version associated with code and configuration
  - each version can run in one or more instances
  - multiple versions can co-exist
  - options to rollback and split traffic
