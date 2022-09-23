
## Overview
### Add-on description
The Kubernetes-csi-tencentcloud CFS-CSI plug-in allows you to use Tencent Cloud File Storage in your TKE cluster.

> ! For clusters of version 1.12, you need to modify the kubelet configuration by adding `\--feature-gates=KubeletPluginsWatcher=false\`.

### Kubernetes objects deployed in a cluster

| Kubernetes Object Name | Type | Default Resource Occupation | Namespace |
| -------------------------- | ------------------------ | ------ | ------------ |
| csi-provisioner-cfsplugin | StatefulSet | - | kube-system |
| csi-nodeplugin-cfsplugin | DaemonSet | - | kube-system |
| csi-provisioner-cfsplugin | Service | 1C2G | kube-system |

## Use Cases
Cloud File Storage (CFS) provides a scalable shared file storage service that can be used with Tencent Cloud services such as CVM, TKE, and BatchCompute. CFS offers standard NFS and CIFS/SMB file system access protocols to provide shared data sources for multiple CVM instances or other computing services. It supports elastic capacity expansion and performance scaling. CFS can be mounted on existing applications without modification. As a highly available and reliable distributed file system, CFS is suitable for various scenarios such as big data analysis, media processing, and content management.

CFS is easy to integrate. You do not need to adjust your business structure or make complex configurations. You can integrate and use CFS in three steps: create a file system, launch a file system client on the server, and mount the created file system. With the CFS-CSI add-on, you can quickly use CFS through the standard native Kubernetes in your TKE cluster. For more information, see [CFS Usage](https://intl.cloud.tencent.com/document/product/582/9129).

## Limits
- For the limits of CFS, see [CFS System Limits](https://intl.cloud.tencent.com/document/product/582/9135).
- To use CFS in TKE, you need to install this add-on in your cluster, which will occupy some system resources.

## Directions
### Installing and setting the CFS add-on

1. Log in to the [TKE Console](https://console.qcloud.com/tke2) and select **Cluster** in the left sidebar.
2. On the "Cluster Management" page, click the ID of the target cluster to go to the cluster details page.
3. In the left sidebar, click **Add-on Management** to go to the "Add-on List" page.
4. On the "Add-on List" page, click **Create**. On the displayed "Create an Add-on" page, select **CFS**.
5. Click **Finish** to create the add-on.



### Creating a CFS-type StorageClass
1. On the "Cluster Management" page, click the ID of the cluster that uses CFS to go to the cluster details page.
2. In the left sidebar, choose **Storage** > **StorageClass** and click **Create** to go to the "Create a StorageClass" page.
3. Create a CFS-type StorageClass based on your actual requirements, as shown in the figure below:
![](https://main.qcloudimg.com/raw/8bd0f5d33ed5a5f3dc7b53f19844b042.png)
4. Click **Create a StorageClass** to complete the creation.

### Creating a PersistentVolumeClaim
1. On the "Cluster Management" page, click the ID of the cluster that uses CFS to go to the cluster details page.
2. In the left sidebar, choose **Storage** > **PersistentVolumeClaim** and click **Create** to go to the "Create a PersistentVolumeClaim" page.
3. Create a CFS-type PersistentVolumeClaim based on your actual requirements and select the StorageClass created above.
4. Click **Create a PersistentVolumeClaim** to complete the creation process.





### Creating a workload
1. On the "Cluster Management" page, click the ID of the cluster that uses CFS to go to the cluster details page.
2. In the left sidebar, choose **Workload** > **Deployment** and click **Create** to go to the "Create a Workload" page.
3. Based on your actual requirements, select **Use an existing PVC** for volumes and select the PVC created above.
4. Mount the PVC to the specified container path and click **Create a Workload** to complete the creation process.


