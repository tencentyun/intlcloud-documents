## Operation Scenario

The CBS-CSI add-on allows you to select the storage class and create the corresponding PVs and PVCs of the CBS type in a TKE cluster on the console. This document introduces the features of the CBS-CSI add-on and some common use cases.


## Features


| Feature | Description |
|---------|---------|
| Static volume | Supports manual creation of volumes, PV objects, and PVC objects. |
| Dynamic volume | Supports configuration, creation, and deletion of volumes and PV objects through StorageClass. |
| Storage topology awareness | CBS does not support cross-AZ mounting. In a cluster with multiple AZs, the CBS-CSI add-on will schedule pods first, and then volumes will be created in the AZ of the node where the pods are scheduled. |
| Scheduler awareness of node maxAttachLimit | By default, one Tencent CVM instance can mount up to 20 cloud disks. When scheduling pods, the scheduler will filter out nodes where the number of mounted cloud disks has exceeded the limit. |
| Online volume expansion | You can modify the PVC capacity field to implement online expansion (only the CBS type is supported). |
| Volume snapshot and restoration | Supports the creation of volumes through snapshots. |


## Component Description


After it is deployed in a cluster, the CBS-CSI add-on contains the following components:

- DaemonSet (NodePlugin): each node provides a DaemonSet. It consists of two containers, CBS-CSI Driver and node-driver-registrar. It is used to register the driver for the node and provide the ability to mount.
- StatefulSet and Deployment (Controller): consists of a driver and multiple sidecars (external-provisioner, external-attacher, external-resizer, external-snapshotter, and snapshot-controller). It provides functions, such as o create or delete volumes, attach or detach, expand, and take snapshot.

![](https://main.qcloudimg.com/raw/f469674c69e02fc912b65d0babc001bd.png)



## Limits

- TKE cluster version 1.14 or later
- You can expand cloud disks online and create snapshots in a TKE cluster only after using the CBS-CSI add-on.
- You can continue to use QcloudCbs (In-Tree plugin) in your TKE cluster. (It will be integrated to CBS-CSI through Volume Migration in the future.)

## Use Cases

- [Avoid attaching cloud disk across availability zones through cbs-csi](https://intl.cloud.tencent.com/document/product/457/45998)
- [Online Expansion of Cloud Disk](https://intl.cloud.tencent.com/document/product/457/45999)

