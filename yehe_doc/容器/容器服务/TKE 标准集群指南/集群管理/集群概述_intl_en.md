## Cluster Overview
A cluster is a collection of cloud resources required for running a container, including several CVMs and CLBs. You can run your applications in your cluster.

## Cluster Architecture

A TKE cluster is compatible with Kubernetes, which includes the following components:
- Master: used to control nodes of the management plane of a cluster.
- Etcd: used to retain the status information of the entire cluster.
- Node: worker nodes used to run applications.

## Cluster Types

TKE supports the following cluster types:

Cluster Type | Description |
|---------|---------|
| Managed cluster | Master and Etcd are managed by TKE |
| Self-deployed cluster | Master and Etcd nodes are built on your owned servers |

For more information, see [Cluster Hosting Mode Instruction](https://intl.cloud.tencent.com/document/product/457/31417).


## Cluster Lifecycle
For more information on TKE cluster lifecycle, see [Cluster Lifecycle](https://intl.cloud.tencent.com/document/product/457/30636).





## Cluster-related Operations

- [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/30637)
- [Changing the Cluster Operating System](https://intl.cloud.tencent.com/document/product/457/42075)
- [Cluster Scaling](https://intl.cloud.tencent.com/document/product/457/30638)
- [Connecting to a Cluster](https://intl.cloud.tencent.com/document/product/457/30639)
- [Upgrading a Cluster](https://intl.cloud.tencent.com/document/product/457/30640)
- [Enabling IPVS for a Cluster](https://intl.cloud.tencent.com/document/product/457/30641)
- [Enabling GPU Scheduling for a Cluster](https://intl.cloud.tencent.com/document/product/457/30642)
- [How to Choose TKE Network Mode](https://intl.cloud.tencent.com/document/product/457/38966)
- [Deleting a Cluster](https://intl.cloud.tencent.com/document/product/457/36280)
- [Custom Kubernetes Component Launch Parameters](https://intl.cloud.tencent.com/document/product/457/38139)
