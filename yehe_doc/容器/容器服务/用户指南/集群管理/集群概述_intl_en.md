## Clusters
A cluster is a collection of cloud resources required for running a container, including several CVMs and CLBs. You can run your applications in your cluster.

## Cluster Architecture

A TKE cluster is compatible with Kubernetes and consists of the following components:
- Master: is used to control the nodes of the management plane of a cluster.
- Etcd: is used to store the status information of the entire cluster.
- Node: serves as a worker node to run applications.

## Cluster Types

TKE container cluster supports the following types:
- CVM container cluster
    + Managed cluster (Master and Etcd are managed by TKE)
    + Independently deployed cluster (Master and Etcd are built on your own servers)

### Managed clusters

#### Mode overview

Tencent Cloud provides the Kubernetes cluster management service for managing Master and Etcd.
In this mode, Master and Etcd of your Kubernetes cluster are managed and maintained in a centralized manner by Tencent Cloud's technical team. You only need to purchase worker nodes for the cluster to run workloads.
>! 
> - The management of Master and Etcd is currently free of charge, but you need to pay for the worker nodes of the cluster, persistent storage, and the CLBs bound to your service.
> - In this mode, Master and Etcd are not user-specific resources. Therefore, you cannot modify their deployment scales or service parameters. If you do need to modify the deployment scales or service parameters, use [independently deployed clusters](#IndependentDeployment) instead.
> - In this mode, because Master always exists, so even if you delete all the worker nodes of the cluster, the cluster will persistently attempt to run the workloads and services that have not been deleted. This process may incur fees. If you want to terminate cluster services and stop incurring fees, delete the cluster.

<span id="IndependentDeployment"></span>
### Independently deployed clusters

#### Mode overview

TKE additionally provides an independent Master deployment mode in which you have full control over your cluster. In this mode, Master and Etcd of the Kubernetes cluster are deployed in your CVM instances, and you have full management and operation permissions on the Kubernetes cluster.

#### Precautions
- This mode is available only for Kubernetes 1.10.x and later.
- You need to purchase resources for deploying Master and Etcd of the Kubernetes cluster.
- If your cluster contains many nodes, we recommend that you select a high-spec CVM model. The following table provides references for model selection.
 <table><tr><th>Cluster Scale</th><th>Recommended Master Node Configuration</th><th>Recommended Node Quantity</th></tr><tr><td>Around 100 nodes</td><td>8 cores and 16-GB SSD system disk</td><td>3 or more</td></tr><tr><td>Around 500 nodes</td><td>16 cores and 32-GB SSD system disk</td><td>3 or more</td></tr><tr><td>1,000 nodes or more</td><td><a href="https://console.cloud.tencent.com/workorder/category/create?level1_id=6&level2_id=350&level1_name=%E8%AE%A1%E7%AE%97%E4%B8%8E%E7%BD%91%E7%BB%9C&level2_name=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1CCS">Contact us</a></td><td>3 or more</td></tr></table>

#### Purchase limits
To ensure the high availability of clusters and services and improve cluster performance, we recommend that you meet the following requirements in independent deployment mode:
 - Deploy at least 3 Master and Etcd nodes.
 - Use a model with at least 4 cores for Master and Etcd nodes.
 - Use SSD disks as system disks of Master and Etcd nodes.

## Notes

To ensure the stability of your cluster and the recovery efficiency in case of exceptions, take the following precautions:
 - In **independent deployment mode**:
  - Do not delete the core components of the Master node that support the running of the Kubernetes cluster.
  - Do not modify the configuration parameters of the core components of the Master node.
  - Do not modify or delete the core resources in the Kubernetes cluster.
  - Do not modify or delete the relevant certificate files (with the .crt or .key file extension) of the Master node.
 - Unless otherwise required:
  - Do not change the Docker version of any node.
  - Do not modify the operating system components, such as kernel and nfs-utils, of any node.

>? 
> - Core components include kube-APIserver, kube-scheduler, kube-controller-manager, tke-tools, systemd, and cluster-container-agent.
> - Configuration parameters of core components include kube-APIserver parameters, kube-scheduler parameters, and kube-controller-manager parameters.
> - Core resources in the cluster include but are not limited to hpa endpoint, master service account, kube-dns, auto-scaler, master cluster role, and master cluster role binding.

## Cluster-Related Operations

- [Creating a cluster](https://intl.cloud.tencent.com/document/product/457/30637)
- [Scaling a cluster](https://intl.cloud.tencent.com/document/product/457/30638)
- [Connecting to a cluster](https://intl.cloud.tencent.com/document/product/457/30639)
- [Enabling IPVS for a cluster](https://intl.cloud.tencent.com/document/product/457/30641)
- [Enabling GPU scheduling for a cluster](https://intl.cloud.tencent.com/document/product/457/30642)
- [CVM container cluster network](https://intl.cloud.tencent.com/document/product/457/30643)
- [BM container cluster network](https://intl.cloud.tencent.com/document/product/457/30644)
