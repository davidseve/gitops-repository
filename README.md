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

### chart-config.json

The `chart-config.json` file is used to specify the Helm chart configuration for deploying applications in Argo CD. This file contains the necessary information to locate and use a specific Helm chart from a Helm repository.

#### Key Fields

- `chart`: The name of the Helm chart to be used. In this case, it is set to `quarkus`.
- `repoURL`: The URL of the Helm chart repository where the chart is hosted. For example, `https://redhat-developer.github.io/redhat-helm-charts`.
- `targetRevision`: The version of the Helm chart to be used. In this example, it is set to `0.0.3`.

#### Example

```json
{
    "chart": "quarkus",
    "repoURL": "https://redhat-developer.github.io/redhat-helm-charts",
    "targetRevision": "0.0.3"
}
```

#### Usage in Argo CD

This file is referenced in the Argo CD ApplicationSet configuration to define the source of the Helm chart for the application. The `chart`, `repoURL`, and `targetRevision` fields are used by Argo CD to fetch and deploy the specified Helm chart.

#### Integration with ApplicationSet

In the `applicationset.yaml` file, the `chart-config.json` file is used to dynamically generate applications for different clusters and environments. The path to this file is specified in the `generators` section of the ApplicationSet configuration.

Example snippet from `applicationset.yaml`:

```yaml
generators:
  - git:
      repoURL: https://github.com/davidseve/gitops-repository.git
      revision: HEAD
      files:
      - path: 00-apps/**/{{.cluster}}/{{.environment}}/chart-config.json
```

This configuration ensures that the correct Helm chart is used for each application deployment based on the cluster and environment.

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