## Overview
Tencent Kubernetes Engine (TKE) allows you to use Cloud File Storage (CFS) by creating persistent volumes (PVs) and persistent volume claims (PVCs) and mounting volumes to workloads. This document describes how to mount a CFS disk to a workload in a cluster by using the following two methods:
- [Method 1: dynamically creating a CFS disk](#dynamicCFS)
- [Method 2: using an existing CFS disk](#alreadyCFS)


## Preparations
### Installing the CFS add-on
>? If your cluster has been installed with the CFS-CSI add-on, skip this step.

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. Click **Cluster** in the left sidebar to go to the **Cluster Management** page.
3. Choose the ID of the cluster for which you want to create an add-on and click **Add-On Management** in the left sidebar on the cluster details page.
4. On the **Add-On Management** page, click **Create** to go to the **Create Add-On** page.
5. Select **CFS** and click **Done**.



## Directions
<span id="dynamicCFS"></span>

### Dynamically creating a CFS disk

To dynamically create a CFS disk, complete the following steps:
1. Create a StorageClass of the CFS type and define a CFS template.
2. Create a PVC by using the StorageClass and further define the CFS parameters.
3. Select the created PVC when creating a workload volume and configure the container mount point.
For more information, see [Managing CFS templates by using a StorageClass](https://intl.cloud.tencent.com/document/product/457/36154).

<span id="alreadyCFS"></span>

### Using an existing CFS disk

To use an existing CFS disk, complete the following steps:
1. Create a PV by using an existing CFS disk.
2. When creating a PVC, set the same StorageClass and capacity as that for the preceding PV.
3. When creating a workload, select the preceding PVC.
For more information, see [Managing CFS by using PVs and PVCs](https://intl.cloud.tencent.com/document/product/457/36155).

## Related Information

For more information on how to use CFS, see [README_CFS.md](https://github.com/TencentCloud/kubernetes-csi-tencentcloud/blob/master/docs/README_CFS.md).
