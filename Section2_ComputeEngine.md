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
