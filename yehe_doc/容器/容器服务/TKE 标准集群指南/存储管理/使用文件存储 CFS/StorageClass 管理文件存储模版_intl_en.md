## Overview
A cluster admin can use StorageClass to define different storage classes for Tencent Kubernetes Engine (TKE) clusters. TKE provides the block storage StorageClass by default. You can use both StorageClass and PersistentVolumeClaim to dynamically create required storage resources.

This document describes how to create a StorageClass of the Cloud File Storage (CFS) type by using the console and Kubectl as well as how to customize the template required by CFS disks.

## Preparations
### Installing the CFS add-on
>? If your cluster has been installed with the CFS-CSI add-on, skip this step.
>
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **Cluster** to go to the **Cluster management** page.
3. Click the ID of the cluster for which you want to create an add-on to go to the **Cluster details** page.
4. Select **Add-On management** > **Create** to go to **Create an add-On** page.
5. On the **Create add-on** page, select **CFS** and click **Complete**.

### Creating a subnet
When creating a StorageClass, you need to set the subnet of CFS. To ensure that all availability zones have suitable subnets in the VPC where the CFS resides, we recommend that you create subnets in advance.

1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1) and click **Subnet** in the left sidebar.
2. On the **Subnet** page, click **Create**. The **Create a subnet** page appears, where you can configure the subnet name, VPC IP range, CIDR block, availability zone, and associated route table, as shown in the following figure.
![](https://main.qcloudimg.com/raw/f95414e493602e4b423e44a15ddc139e.png)
3. (Optional) Click **+New line** to create multiple subnets at a time.
4. Click **Create**.

### Creating a permission group and adding permission group rules
When creating a StorageClass, you need to configure a permission group for CFS. To ensure that CFS has a suitable permission group, we recommend that you create a permission group in advance.

1. Log in to the [CFS console](https://console.cloud.tencent.com/cfs) and click **Permission Group** in the left sidebar.
2. On the **Permission group** page, click **Create**. In the **Create permission group** window that appears, configure the permission group name and remarks.
3. Click **Confirm** to create the permission group. It will now appear on the **Permission group** page.
4. Click the ID of this permission group to go to its details page, where you can add, modify, or delete permission group rules. If no rules have been added to this permission group, all operations are allowed. For more information, see [Creating a permission group rule](https://intl.cloud.tencent.com/document/product/582/10951).

### Getting the file system FSID
1. In the [CFS console](https://console.cloud.tencent.com/cfs/fs?rid=1), click the ID of the file system for which you want to obtain the FSID. The details page of the file system appears.
2. Select the **Mount target info** tab and get the file system FSID next to **Mount to Linux** such as `a43qadkl` as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/9b1933b9a13497fa8964f8e5d13226fb.png)
>? For better stability, when you create a PV by YAML and use the NFSv3 protocol for mounting, you need to specify the FSID of the file system to be mounted.

## Directions
### Console operation instructions

[](id:create)
#### Creating a StorageClass via the console
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cluster** in the left sidebar.
2. On the **Cluster management** page, click the ID of the target cluster to go to the cluster details page.
3. Choose **Storage** > **StorageClass** in the left sidebar to go to the **StorageClass** page, as shown in the following figure.
![](https://main.qcloudimg.com/raw/67c2d9b13758cb8c8b7080ec7b236afc.png)
4. Click **Create** to go to the **Create StorageClass** page, where you can set the parameters as required, as shown in the following figure.
   ![](https://main.qcloudimg.com/raw/b457e1fed71474e3edc4f282da80487f.png)
   The main parameters are described as follows:
   - **Name**: Set a custom name. This document uses `cfs-storageclass`as an example.
   - **Provisioner**: Select **Cloud File Storage**.
   - **Availability zone**: Set the available zones that can use CFS in the current region. Different regions may support different storage classes in different availability zones. For more information, see [Available Regions](https://intl.cloud.tencent.com/document/product/582/35772).
   - **CFS subnet**: Set the subnet range that can be used by CFS in the current availability zone based on your needs.
   - **Storage type**: CFS provides **Standard Storage** and **High-Performance Storage**. Different regions may support different storage types in different availability zones. Select a storage type as prompted by the console.
     - **Standard storage**: This class features low cost and large capacity, and is suitable for applications that are cost-sensitive and need large capacity. For example, standard storage can be used for data backup, file sharing, and log storage.
     - **High-performance storage**: This class features high throughput and high IOPS and is suitable for I/O-intensive workloads. For example, high-performance storage can be used for high-performance computing, media asset rendering, machine learning, DevOps, and office OA.
   - **File service protocol**: NFS is used by default, which allows transparent access to files and file systems on the file server.
   - **Protocol version**: It is recommended to use NFSV3 protocol for mounting. Use NFSV4 protocol if you need to edit a file on multiple CVMs.
   - **Permission group**: Configure a permission group for the file system, which is used to manage the access and read/write permissions of clients that access the file system in the same network. Select an appropriate permission group as required. If no such permission group is available, create one on the [Permission Group](https://console.cloud.tencent.com/cfs/permission) page.
   - **Reclaim policy**: The **Delete** and **Retain** reclaim policies are provided. For data security, we recommend that you select **Retain**.
      - **Delete**: If the PVs are dynamically created through a PVC, when the PVC is terminated, the PVs and the storage instances bound with the PVC are terminated automatically.
      - **Retain**: If the PVs are dynamically created through a PVC, when the PVC is terminated, the PVs and the storage instances bound with it are retained.
   - **Tag**: Select the cloud tag to be bound with the CFS instance. The tag will be automatically inherited by the CFS instance that is created dynamically by StorageClass. When StorageClass is created, the parameters of the tag bound with it cannot be modified. If the existing tags are not suitable, please go to [Tag console](https://console.cloud.tencent.com/tag/taglist) to create one.
5. Click **Create StorageClass** to complete the process.

#### Creating a PVC by using a specified StorageClass[](id:createPVC)
1. On the **Cluster management** page, select the ID of the cluster for which a PVC needs to be created.
2. On the cluster details page, choose **Storage** > **PersistentVolumeClaim** in the left sidebar to go to the **PersistentVolumeClaim** page, as shown in the following figure.
![](https://main.qcloudimg.com/raw/32c83af0e9ca2fe663993bddc9bbe1e1.png)
3. Click **Create** to go to the **Create PersistentVolumeClaim** page, where you can set key PVC parameters as required, as shown in the following figure.
   ![](https://main.qcloudimg.com/raw/044c043388d7920b6aef791d673b07d9.png)
   The main parameters are described as follows:
   - **Name**: Set a custom name. This document uses `cfs-pvc` as an example.
   - **Namespace**: Select **default**.
   - **Provisioner**: Select **Cloud File Storage**.
   - **R/W permission**: CFS only supports multi-server read and write.
   - **StorageClass**: Specify a StorageClass as required. This document uses the `cfs-storageclass` created in the step of [Creating a StorageClass](#create) as an example.
>? 
>- The PVC and PV will be bound to the same StorageClass.
>- If you do not specify a StorageClass, the value of `StorageClass` for the corresponding PVC is empty, and the value of the `storageClassName` field in the corresponding YAML file is a null string.
> 
   - **PersistVolume**: Specify a PersistentVolume as required. In the example in this document, no PersistentVolume is specified.
>? 
>- The system first searches the current cluster to see whether there are PVs that meet the binding rules. If not, the system dynamically creates a PV to be bound based on the PVC and the selected StorageClass.
>- If `StorageClass` is not specified, then `PersistVolume` must be specified.
>- No PersistVolume is specified. For more information, see [PV and PVC Binding Rules](https://intl.cloud.tencent.com/document/product/457/37770).
> 
4. Click **Create PersistentVolumeClaim** to complete the creation process.

#### Creating a workload to use a PVC volume
>? This step creates a Deployment workload as an example.
>
1. On the **Cluster management** page, select the target cluster ID to go to the **Deployment** page of the cluster for which the workload needs to be deployed.
2. Click **Create** to go to the **Create Workload** page. For more information on how to create a workload, see [Creating a Deployment](https://intl.cloud.tencent.com/document/product/457/30662). Then, mount a volume as required, as shown in the following figure.
![](https://main.qcloudimg.com/raw/0ff71649814009bd943042745858275e.png)
  - **Volume (optional)**:
    - **Mount method**: Select **Use existing PVC**.
    - **Volume name**: Set a custom name. This document uses `cfs-vol` as an example.
    - **Select PVC**: Select `cfs-pvc`, which you created in the step of [Creating a PVC](#createPVC).
  - **Containers in the Pod**: Click **Add mount target** to set a mount target.
       - **Volume**: Select the volume `cfs-vol` that you added in this step.
       - **Destination path**: Enter a destination path. This document uses `/cache` as an example.
       - **Sub-path**: Mount only a sub-path or a single file in the selected volume, such as `/data` or `/test.txt`.
3. Click **Create Workload** to complete the process.
>! If you use the PVC mount method of CFS, the volume can be mounted to multiple nodes.

### Kubectl operation instructions

#### Creating a StorageClass
```yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: cfs
parameters:
  vpcid: vpc-xxxxxxxx
  subnetid: subnet-xxxxxxxx
  vers: "3"
  resourcetags: ""
provisioner: com.tencent.cloud.csi.cfs
reclaimPolicy: Delete
volumeBindingMode: Immediate
```

The following parameters can be configured:
| Parameter | Required | Description |
| -- | -- | -- |
| zone | No | It defines the location where the file is stored. |
| pgroupid | No | It defines the permission group for the file storage. |
| storagetype | No | It defaults to standard storage (SD). Valid values: SD (standard storage); HP (high-performance storage). |
| vpcid | Yes | It indicates the ID of the VPC where the file is stored. |
| subnetid | Yes | It indicates the ID of the subnet where the file is stored. |
| vers | Yes | It indicates the version of the protocol used by the add-on to connect to the file system. The dynamically created PVs inherit this parameter. The versions "3" and "4" are supported. |
| resourcetags | Yes | It indicates the cloud tag of the file system. A corresponding Tencent Cloud tag is applied on the generated file system. Multiple tags are separated by commas. For example, "a:b,c:d". |

#### Creating a PVC
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: cfs
  namespace: default
spec:
  accessModes:
  - ReadWriteMany
  resources:
    requests:
      storage: 10Gi
  storageClassName: cfs
  volumeMode: Filesystem
  volumeName: XXX
```

| Parameter | Required | Description |
| -- | -- | -- |
| spec.accessModes | No | The cfs storage supports Multiple-Read-Multiple-Write. |
| spec.resources.requests.storage | Yes | The storage capacity only depends on the type of the file system. |
>? 
> 1. CFS supports expanding the storage capacity of the file system according to the file size. The requests and applications are not interrupted during the expansion. The default CFS instance capacity is 10 GiB, and the upper limit of the capacity depends on the product type. For details, see [System Restrictions](https://intl.cloud.tencent.com/document/product/582/9135).
> 2. The PVs dynamically created through a PVC inherit the parameters configured in StorageClass. The parameters are generated automatically by the storage add-on.
