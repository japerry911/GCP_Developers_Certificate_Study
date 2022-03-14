# Section 6 - Getting Started with Google App Engine

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
  - pricing
    - standard
      - instance hours
    - flexible
      - vCPU, memory, persistent disks
  - scaling
    - standard
      - manual, basic, automatic
    - flexible
      - manual, automatic
  - scaling to zero
    - standard
      - yes
    - flexible
      - no, minimum one instance
  - instance startup time
    - standard
      - seconds
    - flexible
      - minutes
  - rapid scaling
    - standard
      - yes
    - flexible
      - no
  - max request timeout
    - standard
      - 1 to 10 minutes
    - flexible
      - 60 minutes
  - local disk
    - standard
      - mostly (except for Python, PHP), can write to `/tmp`
    - flexible
      - yes, ephemeral, new disk on startup
  - ssh for debugging
    - standard
      - no
    - flexible
      - yes

### Component Hierarchy

![App Engine Hierarchy](./images/app_engine_hiearchy.png 'App Engine Hiearchy')

- application - one app per project
- service(s) - multiple microservices or app components
  - example - frontend and backend would be separate services
  - each service can have different settings
  - earlier called modules
- version(s) - each version associated with code and configuration
  - each version can run in one or more instances
  - multiple versions can co-exist
  - options to rollback and split traffic

### Scaling Instances

- automatic
  - automatically scale instances based on load
  - recommended for continously running workloads
  - auto scale based on:
    - target CPU utilization - configure a CPU usage threshold
    - target throughput utilization - configure a throughput threshold
    - max concurrent requests - configure max concurrent requests an instance can receive
  - configure max instances and min instances
- basic
  - instances are created as and when requests are received
  - recommended for Adhoc Workloads
  - instances are shutdown if zero requests
  - tries to keep costs low
  - high latency is possible
  - not supported by flex environment
  - configure max instances and idle timeout
- manual - configure a specific number of to run
  - adjust number of instances manually over time

### Some gcloud Commands

- `gcloud app services list`
- `gcloud app versions list`
- `gcloud app instances list`
- `gcloud app deploy --version=<version-str>`
- `gcloud app browse --version=<version-str>`
- `gcloud app deploy --version=<version-str> --no-promote`
  - no-promote
    - can deploy new version without splitting traffic to it, will still being going to old version after deployment
- `gcloud app services set-traffic --splits=v3=.5,v2=.5 --split-by=random`
  - split traffic 50% 50% for v3 and v2 version IDs
  - if `--split-by` is not specified as flag, defaults to split by IP address
    - by IP address
    - by cookie
    - by random
