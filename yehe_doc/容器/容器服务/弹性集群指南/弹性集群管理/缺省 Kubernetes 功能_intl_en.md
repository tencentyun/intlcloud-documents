## Description
Elastic Kubernetes Service (EKS) does not contain any cluster nodes, and therefore does not support some native Kubernetes features that depend on nodes, kubelet, and kube-proxy.

## Unsupported Native Kubernetes Features
### Kubernetes versions
EKS does not support Kubernetes version 1.12 and earlier.

### Nodes
You cannot add or manage physical nodes through EKS.

### Workloads
- You cannot deploy workloads of the DaemonSet type through EKS.
- You cannot use hostPath volumes through EKS.

### Services
You cannot deploy services of the NodePort type through EKS.

### Volumes
You cannot use Linux filesystem events with inotify, which is a feature of emptyDir volumes.
