## Notes on Cluster Lifecycle Status

| Status | Description |
|:--:|:--|
| Creating | The cluster is being created and is applying for Tencent Cloud resources. |
| Scaling | The number of nodes in the cluster is being changed or nodes are being added or terminated. |
| Running | The cluster is running normally. |
| Upgrading | The cluster is being upgraded. |
| Deleting | The cluster is being deleted. |
| Abnormal | There are exceptions in the cluster, such as node network inaccessibility. |
| Isolated | The managed cluster is being isolated due to overdue payments exceeding 24 hours. Billing for cluster management has stopped. |


>!TKE is based on Kubernetes and is a declarative service. If you have created IaaS resources such as CLB instances or CBS cloud disks in TKE and no longer need to use them, delete the corresponding Service and PersistentVolumeClaim objects in the [TKE console](https://console.cloud.tencent.com/tke2). If you only delete the load balancers in the CLB console or the cloud disks in the CBS console, TKE will recreate them and fees will continue to be incurred.




