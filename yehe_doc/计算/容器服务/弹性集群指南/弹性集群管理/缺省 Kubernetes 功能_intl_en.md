## Descriptions
Elastic Kubernetes Service (EKS) does not contain any cluster nodes, and therefore does not support some native Kubernetes features that depend on nodes, kubelet, and kube-proxy.

## Unsupported Native Kubernetes Features
### Kubernetes versions
1.12 and lower versions are not supported

### Node
Bare Metal nodes are not supported

### Kernel
Custom kernel parameters that do not start with “net” are not supported

### Workloads
- DaemonSets workloads are not supported 
- hostPath cannot be used as volumes.

### Services
Services of NodePort type cannot be deployed.

### Volume
When emptyDir volume is used, inotify is not supported.
