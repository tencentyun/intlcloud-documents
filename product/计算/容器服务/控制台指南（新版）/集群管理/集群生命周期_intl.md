## Notes on Cluster Lifecycle Status

| Status | Description |
|:--:|:--|
| Creating | The cluster is being created and is applying for cloud resources. |
| Adjusting size | The number of nodes in the cluster is being changed or nodes are being added or terminated. |
| Running | The cluster is running normally. |
| Upgrading | The cluster is being upgraded. |
| Deleting | The cluster is being deleted. |
| Exceptional | There are exceptions in the cluster, such as node network inaccessibility. |

 TKE is based on Kubernetes and is a declarative service. If you have created IaaS resources such as CLB load balancers or CBS cloud disks in TKE and no longer need to use them, please delete the corresponding Service and PersistentVolumeClaim objects in the TKE console. If you only delete the load balancers in the CLB console or the cloud disks in the CBS console, TKE will recreate them and fees will continue to be incurred.
