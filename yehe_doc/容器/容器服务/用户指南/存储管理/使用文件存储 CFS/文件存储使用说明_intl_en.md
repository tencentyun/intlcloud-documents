## Operation Scenarios
Tencent Kubernetes Engine (TKE) allows you to use Cloud File Storage (CFS) by creating persistent volumes (PVs) and persistent volume claims (PVCs) and mounting volumes to workloads. This document describes how to mount a CFS disk to a workload in a cluster by using the following two methods:
- [Method 1: dynamically creating a CFS disk](#dynamicCFS)
- [Method 2: using an existing CFS disk](#alreadyCFS)


## Preparations
### Installing the CFS add-on
>?If your cluster has been installed with the CFS-CSI add-on, skip this step.
 
1. Log in to the [Tencent Kubernetes Engine console](https://console.cloud.tencent.com/tke2) and choose **Add-on** in the left sidebar.
2. On the **Add-on** page, select the cluster that needs to use the CFS add-on and the relevant region, and then click **Create**.
3. On the **Create an add-on** page, select **CFS** and click **Done**.



## Directions
<span id="dynamicCFS"></span>
### Dynamically creating a CFS disk

If you need to dynamically create a CFS disk, you can perform the following steps:
1. Create a StorageClass of the CFS type and define the CFS template to use.
2. Create a PVC by using the StorageClass and further define the CFS parameters.
3. Select the created PVC when creating a workload volume and set the container mount point.

<span id="alreadyCFS"></span>
### Using an existing CFS disk

If you need to use an existing CFS disk, you can perform the following steps:
1. Create a PV by using an existing CFS disk.
2. When creating a PVC, set the same StorageClass and capacity as that for the preceding PV.
3. When creating a workload, select the above PVC.

## Reference

For more information on how to use CFS, see [README_CFS.md](https://github.com/TencentCloud/kubernetes-csi-tencentcloud/blob/master/docs/README_CFS.md).
