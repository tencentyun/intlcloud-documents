## Managed Master Mode

### Overview
Tencent Kubernetes Engine (TKE) provides management services for Kubernetes clusters where Master and Etcd nodes are fully managed.
In this mode, the Master and Etcd nodes of your Kubernetes cluster will be centrally managed and maintained by the Tencent Cloud technical team. You only need to purchase the cluster and run worker nodes required for your business load, with no need to worry about management and maintenance issues.

### Notes on the managed master mode
- TKE charges cluster management fees based on the specifications of the managed clusters, and charges cloud resources (CVM, persistent storage, and CLB) fees based on the actual usage. For more information about the billing modes and prices, see [TKE Billing Overview](https://intl.cloud.tencent.com/document/product/457/45157).
- Master and Etcd nodes in this mode are not user-specific resources. Therefore, you cannot modify their deployment scale and service parameters. If you need to do so, Select the [Independent Master Deployment Mode](#IndependentDeploy).
- In this mode, even if you delete all the worker nodes from the cluster, the cluster will still persistently attempt to run workloads and services that have not been deleted. This process may incur fees. If you need to stop the services and prevent cluster fees, delete the cluster.

[](id:IndependentDeploy)
## Independent Master Deployment Mode
### Overview
TKE also provides an independent Master deployment mode, which gives you full control over your Kubernetes cluster.
In this mode, the Master and Etcd nodes of the Kubernetes cluster are deployed on your Cloud Virtual Machines (CVMs). You have all permissions to manage and operate the Kubernetes cluster.

### Notes on the independent master deployment mode
- This mode is available only for Kubernetes 1.10.x or later.
- You need to purchase resources for deploying Master and Etcd of the Kubernetes cluster.
- If your cluster contains a large number of nodes, it is recommended that you select a high-spec CVM model. The following table provides reference for model selection.
<table><tr><th>Cluster Size</th><th>Recommended Master Node Configuration</th><th>Recommended Node Quantity</th></tr><tr><td>Around 100 nodes</td><td>8-core 16 GB SSD system disk</td><td>Three or more</td></tr><tr><td>Around 500 nodes</td><td>16-core 32 GB SSD system disk</td><td>Three or more</td></tr><tr><td>1,000 nodes or more</td><td><a href="https://console.intl.cloud.tencent.com/workorder/category">Submit a ticket</a></td><td>Three or more</td></tr></table>

### Purchase Requirements
To ensure the high availability of clusters and services and improve cluster performance, it is recommended that you comply with the following requirements in independent deployment mode:
 - Deploy at least 3 Master and Etcd nodes.
 - Use models with at least 4 cores for Master and Etcd nodes.
 - Use SSD disks as system disks of Master and Etcd nodes.

## Notes

To ensure the stability of your cluster and improve failback efficiency, we recommend that you note the following:
 - In the independent Master deployment mode:
  - Do not delete the core components of the Master node that support the operation of the Kubernetes cluster.
  - Do not modify the configuration parameters of the core components of the Master node.
  - Do not modify or delete the core resources in the Kubernetes cluster.
  - Do not modify or delete the relevant certificate files (with .crt and .key extensions) of the Master node.
 - Unless otherwise required:
  - Do not modify the Docker version of any node.
  - Do not modify the OS components, such as kernel and nfs-utils, of any node.

>? 
> - Core components include kube-APIserver, kube-scheduler, kube-controller-manager, tke-tools, systemd, and cluster-container-agent.
> - Configuration parameters of core components include kube-APIserver parameters, kube-scheduler parameters, and kube-controller-manager parameters.
> - Core resources in the cluster (including but not limited to): hpa endpoint, master service account, kube-dns, auto-scaler, master cluster role, and master cluster role binding.

If you have any questions about the above suggestions, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category).

