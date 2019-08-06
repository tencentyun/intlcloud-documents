### Managed Master Mode

### Overview

Tencent Cloud provides Kubernetes cluster management service for Master and Etcd.
With this mode, the Master and Etcd of your Kubernetes cluster will be centrally managed and maintained by Tencent Cloud's technical team. You only need to purchase the cluster and run worker nodes as required by your business load, and do not need to worry about management and maintenance issues. 

### Notes

- Management of Master and Etcd is currently free of charge, but you need to pay for the worker nodes of the cluster, persistent storage, and service-bound load balancers.
- Master and Etcd in this mode are not user-specific resources; therefore, you cannot modify their deployment scale and service parameters. If you need to do so, please use [independent master deployment mode](#IndependentDeploy).
- In this mode, even if you delete all the working nodes of the cluster, the cluster will persistently attempt to run workloads and services that have not been deleted. In this process, you may incur fees. If you need to terminate cluster services and stop incurring fees, please delete the cluster.

<span id="IndependentDeploy"></span>
## Independent Master Deployment Mode

### Overview

TKE also provides an independent deployment mode where you can control the Master on your own. In this mode, the Master and Etcd of the Kubernetes cluster will be deployed on the CVM instances you purchased, and you will have all administrative and operational permissions for the Kubernetes cluster.

> - This mode is only available for Kubernetes v1.10.x or higher.
> - In this mode, you need to purchase additional resources for deployment of Master and Etcd of the Kubernetes cluster.
> - If you have a cluster, we recommend selecting a high-spec model. For model selection, see below for reference:
> <table><tr><th>Cluster size</th><th>Recommended Master node configuration</th><th>Recommended node quantity</th></tr><tr><td>Around 100 nodes</td><td>8-core 16 GB SSD system disk</td><td>Over 3</td></tr><tr><td>Around 500 nodes</td><td>16-core 32 GB SSD system disk</td><td>Over 3</td></tr><tr><td>1,000+ nodes</td><td><a href="https://console.cloud.tencent.com/workorder/category/create?level1_id=6&level2_id=350&level1_name=%E8%AE%A1%E7%AE%97%E4%B8%8E%E7%BD%91%E7%BB%9C&level2_name=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1CCS">Contact us</a></td><td>Over 3</td></tr></table>

### Notes

To ensure high availability of clusters and services and improve cluster performance, apply the following restrictions in the independent deployment mode:
 - At least 3 Master and Etcd nodes must be deployed.
 - For Master and Etcd nodes, models with at least 4 cores are required.
 - The Master and Etcd nodes must use SSD disks as the system disk.

## Considerations

To ensure the stability of your cluster and improve recovery efficiency in case of exceptions, we recommend:
 - In independent deployment mode, do not delete the core components of the Master node that support Kubernetes running.
 - In independent deployment mode, do not modify the configuration parameters of the core Master components.
 - In independent deployment mode, do not modify or delete the core resources in the cluster.
 - In independent deployment mode, do not modify or delete the relevant certificate files (with .crt or .key extension) of the Master node.
 - Do not modify the docker version of any node unless absolutely necessary.
 - Do not modify any components related to kernel and nfs-utils of the OS of any node unless absolutely necessary.


> - Core components: kube-APIserver, kube-scheduler, kube-controller-manager, tke-tools, systemd, cluster-container-agent.
> - Core component configuration parameters: kube-APIserver parameters, kube-scheduler parameters, kube-controller-manager parameters.
> - Core resources in the cluster (including but not limited to): hpa endpoint, master service account, kube-dns, auto-scaler, master cluster role, master cluster role binding.

If you have any questions, please [contact us](https://console.cloud.tencent.com/workorder/category/create?level1_id=6&level2_id=350&level1_name=%E8%AE%A1%E7%AE%97%E4%B8%8E%E7%BD%91%E7%BB%9C&level2_name=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1CCS).
