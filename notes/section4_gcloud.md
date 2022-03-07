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
