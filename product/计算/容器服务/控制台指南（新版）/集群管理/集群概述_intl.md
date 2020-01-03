## Cluster Overview

A cluster is a collection of cloud resources required by container operation, including several CVM instances, load balancers, and other Tencent Cloud resources. You can run your applications in the cluster.

## Cluster Architecture

A TKE cluster is compatible with Kubernetes, which includes the following components:
- Master: Used to control the managing node of a cluster.
- Etcd: Used to retain the status information of the entire cluster.
- Node: This is the working node where the business is run.

## Cluster Type

TKE supports the following two cluster types:
- CVM container cluster
    + Managed cluster (Master and Etcd are managed by TKE)
    + Independently deployed cluster (Master and Etcd are built on your owned servers)
- CPM container cluster (which can be applied for by submitting a ticket)

### Managed Cluster

#### Mode Overview

Tencent Cloud provides Kubernetes cluster management service for managing Master and Etcd.
In this service mode, the Master and Etcd of your Kubernetes cluster will be managed and maintained by Tencent Cloud's technical team. You only need to purchase the working nodes required to run the load, and don't need to take care of cluster management.


> - Management of Master and Etcd is currently free of charge, but you need to pay for the working nodes of the cluster, persistent storage, and load balancing.
> - Master and Etcd in this mode are not user-specific resources; therefore, you cannot modify their deployment scale and service parameters. If you need to modify the deployment scale and service parameters of Master and Etcd, please use an [independently deployed cluster](#IndependentDeployment).
> - In this mode, because the Master always exists, even if you delete all the working nodes of the cluster, the cluster will still continue to try running your workloads and services that have not been deleted. In this process, fees may be incurred. If want need to terminate cluster services and stop incurring fees, please delete the cluster directly.

<span id="IndependentDeployment"></span>

### Independently Deployed Cluster

#### Mode Overview

TKE also provides an independent deployment mode where you can control the Master on your own. In this mode, the Master and Etcd of the Kubernetes cluster will be deployed on the CVM instances you purchase. You have all the administrative and operational permissions of the cluster.


> - This mode is only available for Kubernetes v1.10.x or higher.
> - In this mode, you need to purchase additional resources for deployment of Master and Etcd of the Kubernetes cluster.
> - If your cluster is large, it is recommended to select a high-spec model. For model selection, see below for reference:
> <table><tr><th>Cluster size</th><th>Recommended Master node configuration</th><th>Recommended node quantity</th></tr><tr><td>Around 100 nodes</td><td>8-core 16 GB SSD system disk</td><td>Over 3</td></tr><tr><td>Around 500 nodes</td><td>16-core 32 GB SSD system disk</td><td>Over 3</td></tr><tr><td>1,000+ nodes</td><td><a href="https://console.cloud.tencent.com/workorder/category/create?level1_id=6&level2_id=350&level1_name=%E8%AE%A1%E7%AE%97%E4%B8%8E%E7%BD%91%E7%BB%9C&level2_name=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1CCS">Contact us</a></td><td>Over 3</td></tr></table>

#### Notes on Master Purchase Restrictions

To ensure high availability of clusters and services and improve cluster performance, the following restrictions apply in the independent deployment mode:
 - At least 3 Master and Etcd nodes must be deployed.
 - For Master and Etcd nodes, models with at least 4 cores are required.
 - The Master and Etcd nodes must use SSD disks as the system disk.

## Precautions

In order to ensure the stability of your cluster and the recovery efficiency in case of exceptions, the following suggestions should be noted:
 - In independent deployment mode, do not delete the core components of the Master node that support Kubernetes running.
 - In independent deployment mode, do not modify the configuration parameters of the core Master components.
 - In independent deployment mode, do not modify or delete the core resources in the cluster.
 - In independent deployment mode, do not modify or delete the relevant certificate files (with .crt or .key extension) of the Master node.
 - Do not modify the docker version of any node unless absolutely necessary.
 - Do not modify any components related to kernel and nfs-utils of the OS of any node unless absolutely necessary.


> - Core components: kube-APIserver, kube-scheduler, kube-controller-manager, tke-tools, systemd, cluster-contrainer-agent.
> - Core component configuration parameters: kube-APIserver parameters, kube-scheduler parameters, kube-controller-manager parameters.
> - Core resources in the cluster (including but not limited to): hpa endpoint, master service account, kube-dns, auto-scaler, master cluster role, master cluster role binding.

## Cluster-related Operations

<!--- [Creating a cluster](https://intl.cloud.tencent.com/document/product/457/30637)-->
- [Scaling a Cluster](https://intl.cloud.tencent.com/document/product/457/30638)
- [Connecting to a cluster](https://intl.cloud.tencent.com/document/product/457/30639)
- [Upgrading a cluster](https://intl.cloud.tencent.com/document/product/457/30640)
- [Enabling IPVS for a cluster](https://intl.cloud.tencent.com/document/product/457/30641)
- [Enabling GPU scheduling for a cluster](https://intl.cloud.tencent.com/document/product/457/30642)
- [CVM container cluster network](https://intl.cloud.tencent.com/document/product/457/30643)
