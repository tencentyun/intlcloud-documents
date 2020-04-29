## Note
Elastic Kubernetes Service (EKS) does not contain any cluster nodes, and therefore does not support some native Kubernetes features that depend on nodes, kubelet, and kube-proxy.

## Unsupported Native Kubernetes Features
### Kubernetes versions
1.12 and lower versions are not supported

### Nodes
Bare Metal nodes are not supported

### Workloads
- DaemonSets workloads are not supported 
- hostPath cannot be used as volumes.

### Services
Services of NodePort type cannot be deployed.

### Volumes
When emptyDir volume is used, inotify is not supported.
