# Section 2 - Google Compute Engine

### Introduction

- virtual machines - virtual servers in GCP
- Google Compute Engine (GCE) - provision and manage virtual machines
- features
  - create and manage lifecycle of VM instances
  - load balancing and auto scaling for multiple VM instances
  - attach storage and network storage
  - manage network connectivity and configuration for your VM instances

### Machine Types and Images in GCE

- machine families - what type of hardware do you want to run your workloads on?
  - general purpose (E2, N2, N2D, N1) - best price-performance ratio
    - web and application servers, small-medium databases, dev environments
  - memory optimized (M2, M1) - ultra high memory workloads
    - large in-memory databases and in-memory analytics
  - compute optimized (C2) - compute intensive workloads
    - gaming applications
- machine types - how much CPU, memory, or disk do you want?
  - variety of machine types are available for each machine family
  - example
    - `e2-standard-2`
      - e2 - machine type family
      - standard - type of workload
      - 2 - number of CPUs
  - memory, disk, and networking capabilities increase along with vCPUs
- image - what operating system and what software do you want on the instance?
  - type of images
    - public images
      - provided & maintained by Google or Open Source communities or third party vendors
    - custom images
      - created by you for your projects

### HTTP Webserver

- install apache
  - `apt install apache2`
- content is displayed from `/var/www/html/index.html`

### Internal and External IP Addresses

- external (public) IP addresses are internet addressable
- internal (private) IP addresses are internal to a corporate network
- you **cannot** have two resources the same public (external) IP address
  - **however**, two different corporate networks can have resources with same internal (private) IP address
- all VM instances are assigned at least one internal IP address
- creation of external IP addresses can be enabled for VM instances
  - when you stop a VM instance, the external IP address is lost
    - I believe you can reserve/keep consisent external IP addresses through VPC network serivce
- Static IP addresses
  - how do you get?
    - assign a static IP address to the VM
  - can be switched to another VM instance in the same project

### Compute Engine Simplified Setup

- startup script
  - bootstrapping
    - install OS patches or software when a VM instance is launched
- instance templates
  - define machine type, image, labels, startup script, and other properties into easy-to-use template
  - used to create VM instances and managed instance groups
  - convenient way to create similiar instances
  - cannot be updated
    - to make a change, copy an existing template and modify it

### Reducing Launch Time with Custom Image

- installing OS patches and software at launch of VM instances nicreases boot up time
  - solution: creating a custom image with OS patches and software pre-installed
- can be created from an instance, a persistent disk, a snapshot, another image, or a file in Cloud Storage
- can be shared across projects
- deprecate old images (& specify replacement image)
- hardening an image - customize images to your corporate security standards
- prefer using custom image to startup script
- never create image from disk with running instance

### Reducing Costs

- sustained use discounts
  - automatic discounts for using resources for long periods of time
- commited use discounts
  - reserve compute instances ahead of time
  - commit for 1 year or 3 years
  - up to 70% discount on machine type and GPUs
- preemptible VMs
  - cheaper, temporary instances for non-crtical workloads
  - fixed pricing, max 24 hrs, cheapest

### Compute Engine: Live Migration & Availability Policy

- how do you keep your VM instances running when a host system needs to be updated (a software or a hardware update needs to be performed)?
  - Live Migration
    - your running instance is migrated to another host in the same zone automatically
    - does not change any attirutes or properties of the VM
    - supported for instances with local SSDs
    - not supported for GPUs and preempitble instances
  - important configuration - **Availability Policy**
    - on host maintenace - what should happen during periodic infrastructure maintenance?
      - migrate (default) - migrate VM instance to other hardware
      - terminate - stop the VM instance
    - automatic restart restart VM instances if they are terminated due to non-user-initiated reasons (maintenance events, hardware failure, etc...)

### Best Practices - VMs

- choose zone and region based on
  - cost
  - regulations
  - availability needs
  - latency
  - specific hardware needs
- choose right machine type for your needs
  - play with them to find out the right machine type
- reverse for committed use discounts for constant workloads
- use preemptible instances for fault-tolerant, non time critical workloads
- use labels to indicate environment, team, business unit, etc...

### Compute Engine Scenarios

- what are the pre-requisites to be able to create a VM instance?
  - project
  - billing account
  - compute engines API should be enabled
- you want dedicated hardware for your compliance, licensing, and management needs
  - sole-tenant nodes
- I have 1000s of VMs and I want to automate OS patch managaement, OS inventory management, and OS configuration management (manage software installed)
  - use "VM Manager"
    - OS Patch Management
- You want to login to your VM instance to install software
  - you can SSH into it
- you do not want to expost a VM to internet
  - do not assign an external IP address
- you want to allow HTTP traffic to your VM
  - configure Firewall rules
