## Overview
Tencent Cloud Tencent Kubernetes Engine (TKE) allows you to use Cloud Block Storage (CBS) disks by creating PersistentVolumes (PVs) and PersistentVolumeClaims (PVCs) and mounting volumes to workloads. This document describes how to mount a CBS disk to a workload in a cluster by using the following two methods:
>? When CBS is used through PV and PVC, a cloud disk only supports the creation of one PV, and it can only be mounted by one cluster node at any time.
>
- [Method 1: dynamically creating a CBS disk](#dynamicCBS)
- [Method 2: using an existing CBS disk](#getCBS)

## Directions
### Dynamically creating a CBS disk[](id:dynamicCBS)

To dynamically create a CBS disk, you generally need to complete the following steps:
1. Create a StorageClass of the CBS type and define a CBS template.
>?
>- TKE provides a default StorageClass named cbs, which is configured with a Premium Cloud Storage cloud disk in a randomly selected availability zone in pay-as-you-go mode.
>- You can customize a StorageClass as required.
2. Create a PVC by using the StorageClass and further define the CBS parameters.
3. Select the created PVC when creating a workload volume and set the container mount point.
For more information, please see [Managing CBS templates by using a StorageClass](https://intl.cloud.tencent.com/document/product/457/36158).


### Using an existing CBS disk[](id:getCBS)

You can use an existing CBS disk as follows:
1. Use an existing CBS disk to create a PV.
2. When creating a PVC, use the same StorageClass and capacity as that for the existing PV.
3. When creating a workload, select the PVC.
For more information, please see [Managing CBS by using PVs and PVCs](https://intl.cloud.tencent.com/document/product/457/36159).

