## Managed Master Deployment Mode

### Introduction
Tencent Kubernetes Engine (TKE) provides management services for Kubernetes clusters where Master and Etcd nodes are fully managed.
In this mode, the Master and Etcd nodes of your Kubernetes cluster will be centrally managed and maintained by the Tencent Cloud technical team. You only need to purchase the cluster and run worker nodes required for your business load, with no need to worry about management and maintenance issues.

### Notes on the managed master deployment mode
- The hosting of Master and Etcd nodes is currently free of charge. However, you need to pay for the worker nodes in the cluster, persistent storage, and load balancers bound to your services.
- Master and Etcd nodes in this mode are not user-specific resources. Therefore, you cannot modify their deployment scale and service parameters. If you need to do so, please select the [Independent Master Deployment Mode](#IndependentDeploy).
- In this mode, even if you delete all the worker nodes from the cluster, the cluster will still persistently attempt to run workloads and services that have not been deleted. This process may incur fees. If you need to stop the services and prevent cluster fees, please delete the cluster.

<span id="IndependentDeploy"></span>
## Independent Master Deployment Mode
### Introduction
TKE also provides an independent master deployment mode, which gives you full control over your Kubernetes cluster.
In this mode, the Master and Etcd nodes of the Kubernetes cluster are deployed on your Cloud Virtual Machines (CVMs), and you have all permissions to manage and operate the Kubernetes cluster.

### Notes on the independent master deployment mode
- This mode is only available for Kubernetes v1.10.x and later.
- In this mode, you need to purchase additional resources to deploy the Master and Etcd nodes of the Kubernetes cluster.
- If your cluster contains a large number of nodes, we recommend that you select a high-spec model for the CVMs. When selecting models, see the following table for reference:
<table><tr><th>Cluster size</th><th>Recommended system disk configuration for the Master node</th><th>Recommended number of CVMs</th></tr><tr><td>Approximately 100 nodes</td><td>8-core 16 GB SSD</td><td>>3</td></tr><tr><td>Approximately 500 nodes</td><td>16-core 32 GB SSD</td><td>>3</td></tr><tr><td>More than 1,000 nodes</td><td><a href="https://console.cloud.tencent.com/workorder/category/create?level1_id=6&level2_id=350&level1_name=%E8%AE%A1%E7%AE%97%E4%B8%8E%E7%BD%91%E7%BB%9C&level2_name=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1CCS">Contact us</a></td><td>>3</td></tr></table>

### Purchase Requirements
To ensure the high availability and performance of your cluster and services, you need to meet the following requirements in independent deployment mode:
 - At least three CVMs are deployed for the Master and Etcd nodes.
 - The model of the CVMs configured for Master and Etcd nodes contains at least 4 cores.
 - SSDs are deployed as system disks on the CVMs for the Master and Etcd nodes.

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

> 
> - Core components: kube-APIserver, kube-scheduler, kube-controller-manager, tke-tools, systemd, and cluster-container-agent.
> - Core component configuration parameters: kube-APIserver parameters, kube-scheduler parameters, and kube-controller-manager parameters.
> - Core resources in the cluster (including but not limited to): hpa endpoint, master service account, kube-dns, auto-scaler, master cluster role, and master cluster role binding.

If you have any questions, please [contact us](https://console.cloud.tencent.com/workorder/category/create?level1_id=6&level2_id=350&level1_name=%E8%AE%A1%E7%AE%97%E4%B8%8E%E7%BD%91%E7%BB%9C&level2_name=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1CCS).
