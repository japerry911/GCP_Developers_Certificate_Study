# Section 1 - Getting Started

### Introduction

- before the cloud
  - peak load provisioning
    - buy infrastructure for peak load
    - what would the infrastructure be doing during low loads?
      - would be sitting idle
  - challenges
    - high cost of procuring infastructure
    - need infrastructure maintenance team
- with cloud
  - renting resources when we want them
    - on-demand resource provisioning
  - elasticity
    - ability to swiftly scale the usage of resources up and down to adapt to changing resource demands and dynamically meet workload requirements
- advantages with cloud
  - trade capital expense for variable expense
  - benefit from massive economics of scale
  - stop guessing capacity
  - stop money running and maintaining data centers
  - go global in minutes
- Google Cloud Platform (GCP)
  - one of top 3 cloud providers
  - reliable, secure, and highly-performant
  - "cleanest cloud"
    - net carbon neutral

### Regions and Zones

- high latency - slow access
- low availability - if data center crashes you have this
- regions
  - GCP provides 20+ regions around the world
  - specific geographical location to host your resources
  - advantages
    - high availability
    - low latency
    - global footprint
    - adhere to government regulations
- zones
  - each region has 3 or more zones
  - advantages
    - increased availability and fault tolerance within same region
  - each zone has 1 or more discrete clusters
    - cluster - distinct physical infrastructure that is housed in a data center
  - zones in a region are connected through low-latency links
