# Getting Started with gcloud

### General gcloud Notes

- command line interface to interact with Google Cloud Resources
- most GCP services can be managed from CLI using gcloud
  - compute engine virtual machines
  - managed instance groups
  - databases
  - etc...
- you can create/delete/update/read existing resources and perform actions like deployments as well
- some GCP services have specific CLI tools
  - GCS - gsutil
  - BQ - bq
  - Bigtable - cbt
  - Kubernetes - kubectl
    - gcloud used to manage clusters
- installation
  - part of Google Cloud SDK
    - requires Python
  - you can use gcloud from Cloud Shell with GCP UI
- connecting to GCP
  - `gcloud init`
- gcloud command structure
  - `gcloud <group> <subgroup> <action> ...`
    - group - config or compute or container or dataflow or functions or iam, etc...
    - subgroup - instances or images or instance-templates or machine-types or regions or zones
    - action - create or list or start or stop or describe, etc...
- backed up by a VM instance
  - automatically provisioned by Google Cloud when you launch Cloud Shell
    - 5GB of free persistent disk storage is provided as your $HOME directory
    - prepackaged with latest version of Cloud SDK, Docker, etc...
    - instance is terminated if you are inactive for more than 20 minutes
    - after 120 days of inactivity, even your $HOME directory is deleted
