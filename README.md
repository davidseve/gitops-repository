# GitOps Repository Documentation

## Overview

This repository contains the configuration for deploying applications using Argo CD and Helm. The structure is organized to manage multiple clusters and environments.

## Repository Structure

```
apps/
  app1/
    base/
      values.yaml
    cluster1/
      values.yaml    
      dev/
        values.yaml
clusters/
  cluster1/
    dev/
      values.yaml
    values.yaml
argo-cd-multicluster/
  apps/
    applicationset-app1.yaml
```

### Directory Descriptions

#### apps

Contains application-specific configurations.
  - `app1/`: Configuration for `app1`.
    - `base/`: Base Helm values for `app1`.
    - `cluster1/`: Cluster-specific configurations for `cluster1`.
      - `dev/`: Environment-specific configurations for `dev` environment in `cluster1`.

#### clusters

Contains cluster-specific configurations.
  - `cluster1/`: Configuration for `cluster1`.
    - `dev/`: Environment-specific configurations for `dev` environment in `cluster1`.

- 

#### argo-cd

Contains multi-cluster Argo CD configurations.
  - `apps/`: ApplicationSet configurations for multiple clusters.

## Usage

### Deploying Applications

1. Ensure Argo CD is installed and configured in your Kubernetes cluster.
2. Apply the ApplicationSet configuration for `app1`:

```sh
kubectl apply -f argo-cd/apps/applicationset.yaml
```

## Contributing

Please submit issues and pull requests to contribute to this repository.

---

This documentation provides an overview of the repository structure, configuration files, and usage instructions for deploying applications using Argo CD and Helm.