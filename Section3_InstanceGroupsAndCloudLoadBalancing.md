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
