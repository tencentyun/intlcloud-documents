## Overview

### Add-on description

Helm is a packaging tool for managing Kubernetes applications. For more information, see the [official Helm documentation](https://helm.sh/). TKE integrates Helm-related features, providing visualized CRUD features for Helm Chart on specified clusters.

### Kubernetes objects deployed in a cluster

Deploying Helm Add-on in a cluster will deploy the following Kubernetes objects in the cluster:

| Kubernetes Object Name             | Type                       | Default Resource Occupation | Namespaces |
| -------------- | ---------- | ---------------- | ------------ |
| swift          | deployment | 0.03 core CPU, 20MiB memory | kube-system  |
| tiller-deploy  | deployment | 0.15 core CPU, 80MiB memory | kube-system  |


## Limits
- Supports clusters with Kubernetes version 1.8 and above.
- Occupied cluster resources are 0.28 core CPU and 180 MiB of memory.

## Usage
 For more information, see [Helm Application Management](https://intl.cloud.tencent.com/document/product/457/30683).
