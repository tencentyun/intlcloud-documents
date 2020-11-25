## Overview
### Add-on description
The Kubernetes-csi-tencentcloud COS-CSI plug-in allows you to use Tencent Cloud Object Storage (COS) in your TKE cluster.


### Kubernetes objects deployed in a cluster


| Kubernetes Object Name | Type | Default Resource Consumption | Namespaces |
| -------------------------- | ------------------------ | ------ | ------------ |
| csi-cosplugin-external-runner | StatefulSet | - | kube-system |
| csi-coslauncher | DaemonSet | - | kube-system |
| csi-cosplugin | DaemonSet | - | kube-system |
| csi-cosplugin-external-runner | Service | - | kube-system |
| csi-cos-tencentcloud-token | Secret | - | kube-system |

## Use Cases

COS is a distributed storage service provided by Tencent Cloud to store massive files. You can store and view data at any time over a network. Tencent Cloud COS provides scalable, affordable, reliable, and secure data storage services for all users.

With the COS-CSI add-on, you can quickly use COS as COSFS in your cluster through standard native Kubernetes. For more information, see [COSFS](https://intl.cloud.tencent.com/document/product/436/6883).

## Limits

- Supports clusters with Kubernetes version 1.10 and later.
- For Kubernetes 1.12 clusters, the following kubelet configuration must be added: `--feature-gates=KubeletPluginsWatcher=false`.
- For more information on the limits of COSFS, see [COSFS](https://intl.cloud.tencent.com/document/product/436/6883#.E5.B1.80.E9.99.90.E6.80.A7).
- To use COS in TKE, you must install this add-on in your cluster, which consumes some system resources.



## Usage

### Installing the COS add-on

1. Log in to the [TKE console](https://console.qcloud.com/tke2) and select **Cluster** in the left sidebar.
2. On the "Cluster Management" page, click the ID of the target cluster to go to the cluster details page.
3. In the left sidebar, click **Add-On Management** to go to the "Add-On List" page.
4. On the "Add-On List" page, click **Create**. On the "Create an Add-On" page that appears, select **COS**.
5. Click **Finish** to create the add-on.


### Using COS
You can mount COS for workloads in a TKE cluster. For more information, see [Using COS](https://intl.cloud.tencent.com/document/product/457/36160).

