# Section 3 - Getting Started with Instance Groups and Cloud Load Balancing in Google Cloud

### Instance Groups

- how do you create a group of VM instances
  - instance group
    - group of VM instances managed as a single entity
      - manage group of similar VMs having similar lifecycle as ONE UNIT
- two types of instance groups
  - managed
    - identical VMs created using a template
      - features
        - auto scaling
        - auto healing
        - managed releases
  - unmanaged
    - different configurations for VMs in same group
      - does not offer auto scaling, auto healing, and other services
        no recommended unless you need different kinds of VMs
- location can be zonal or regional
  - regional gives you higher availability

### Managed Instance Groups (MIG)

- identical VMs created using an instance template
- important features
  - maintain certain number of instances
    - if an instance crashes, MIG launches another instance
  - detect applications using health checks (self healing)
  - increase and decrease instances based on load (auto scaling)
  - add load balancer to distribute load
  - create instances in multiple zones (regional MIGs)
    - regional MIGs provide higher availability compared to zonal MIGs
  - releases new application versions without downtime
    - rolling updates
      - release new version step by step (gradually), update a percentage of instances to the new version at a time
    - canary deployment
      - test new version with a group of instances before releasing it across all instances
- creating
  - instance template is mandatory
  - configure auto scaling to automatically adjust number of instances based on load
    - minimum number of instances
    - maximum number of instances
    - autoscaling metrics: CPU utilization target or load balancer utilization target or any other metric from StackDriver
      - cool-down period
        - how long to wait before looking at auto scaling metric again
      - scale in controls
        - prevents a sudden in number of VM instances
          - example
            - don't scale more than 10% of 3 instances in 5 minutes
    - autohealing
      - configure a health check with initial delay
        - how long should you wait for your app to initialize before running a health check?
- updating
  - rolling update
    - gradual update of instances in an instance group to the new instance template
      - specify new template
        - optional, specify template for canary testing
      - specify how you want update to be done
        - when should the update happen
          - start immediately (proactive) or when instance group is resized later (opportunistic)
        - how should update happen
          - maximum surge
            - how many instaces are added at any point in time
          - maximum unavailable
            - how many instances can be offline during the update
  - rolling restart/replace
    - gradual restart or replace of all instances in the group
      - no change in template, but replace/restart existing VMs
      - configure maximum surge, maximum unavailable, and what you want to do (restart/replace)

### Cloud Load Balancing

- distributes user traffic across instances of an application in single region or multiple regions
  - fully distributed, software defined managed service
  - features
    - health check
      - route to healthy instances
        - recovery from failrues
    - auto scaling
    - global load balancing with single anycast IP
      - also supports internal load balancing
- enables
  - high availability
  - auto scaling
  - resiliency
- types
  - HTTP(S)
    - 3 parts
      1. Backend Configuration
      2. Host and Path Rules
      3. Frontend Configuration
  - TCP
  - UDP
    - only single region
- terminology
  - backend
    - group of endpoints that receive traffic from a Google Cloud load balancer (example: instance groups)
    - microservices will most likely have multiple backends
  - frontend
    - specify an IP address, port, and protocol. This IP address is the frontend IP for your client's requests
      - for SSL, a certificate must also be assigned
  - Host and Path Rules
    - specific for HTTP(S) load balancing
    - define rules redirecting the traffic to different backends
      - based on path - in28.com/a vs in28.com/b
      - based on host - a.in28.com vs b.in28.com
      - based on HTTP headers
        - authorization headers
        - methods
  - SSL/TLS termination/offloading
    - client to load balancer: over internet
      - HTTPS recommended
    - load balancer to VM instance: through Google internal network
      - HTTP is ok, HTTPS is still preferred though
    - SSL/TLS termination/offloading
      - client to load balancer: HTTPS/TLS
      - load balancer to VM instance: HTTP/TCP
- choosing a load balancer
  - are we serving external customers / exposing application on internet, or is application internal?
    - external
      - HTTP/HTTPS traffic
        - must use HTTP(S) load balancing
      - TCP traffic
        - if you want SSL offloading/termination
          - SSL proxy
        - if you do not want SSL offloading/termination
          - if you want Global Load Balancing or IPv6
            - TCP proxy
          - if you do not want Global Load Balancing or IPv6
            - if you want end application(s) to see the request as it is coming from user
              - Network TCP/UDP load balancing
            - if you do not want end application(s) to see the request as it is coming from user
              - TCP proxy
      - UDP traffic
        - Network TCP/UDP load balancing
    - internal
      - TCP traffic
        - internal TCP/UPD load balancing
      - UDP traffic
        - internal TCP/UPD load balancing
      - HTTP or HTTPS traffic
        - internal HTTP(S) load balancing

### Scenarios

- you want only healthy instances to receive traffic
  - configure health check
- you want high availability for your VM instances
  - create multiple Managed Instance Groups (MIGs) for your VM instances in multiple regions. Load balance using a load balancer
- you want to route requests to multiple microservices using the same load balancer
  - create individual MIGs and backends for each microservice. Create Host and Path rules to redirect to specific microservice backend based on the path (/microservice-a, /microservice-b, etc...). You can route to backend Cloud Storage bucket as well
- you want to load balance Global external HTTPS traffic across backend instances, across multiple regions
  - choose external HTTP(S) load balancer
- you want SSL termination for Global non-HTTPS traffic with load balancing
  - SSL Proxy Load Balancer
