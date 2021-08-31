Cluster storage management is an important part of preserving business data. At present, Tencent Kubernetes Engine (TKE) supports multiple classes of storage.

## Storage Class
| Storage Class | Description | Usage |
|---|---|---|
| Tencent Cloud Block Storage (CBS) | CBS provides persistent storage at the data block level. It is typically used as the primary storage device for data that requires frequent and fine-grained updates (such as file systems and databases), and it’s featured with high availability, reliability, and performance. | Create persistent volumes (PVs) and persistent volume claims (PVCs), and then mount dynamic or static volumes to workloads. For more information, see [Using CBS](https://intl.cloud.tencent.com/document/product/457/36157). |
| Tencent Cloud File Storage (CFS) | CFS provides standard NFS and CIFS/SMB file system access protocols as well as shared data sources for multiple CVM instances or other computing services. It supports elastic capacity and performance expansion. As a highly available and reliable distributed file system, CFS is suitable for scenarios such as big data analysis, media processing, and content management. | Creat PVs and PVCs, and then mount dynamic or static volumes to workloads. For more information, see [Using CFS](https://intl.cloud.tencent.com/document/product/457/36153). |
| Tencent Cloud Object Storage (COS) | COS is a distributed storage service provided by Tencent Cloud for massive file storage. You can use COS to upload, download, and manage files in different formats. | Create  PVs and PVCs, and then mount static volumes to workloads. |
| Others | - | TKE also supports the following following local storage options for workloads: host path, NFS disk, ConfigMap, and Secret. For more information, see [Volume Management](https://intl.cloud.tencent.com/document/product/457/30678). |



>? We recommend that you use the cloud storage service. Otherwise, when a node encounters an exception and cannot be restored, the locally stored data cannot be restored.


## Related Concepts
- **PersistentVolume (PV)**: this is a storage resource in a cluster. A PV is independent of the pod lifecycle. You can create PVs of different types depending on the StorageClass type.
- **PersistentVolumeClaim (PVC)**: this is a request for storage in a cluster. For example, if a PV is a node resource used by a pod, the PVC states that the PV resource is used. If PV resources are insufficient, the PVC can create a PV dynamically.
