## Overview
A cluster admin can use StorageClass to define different storage classes for Tencent Kubernetes Engine (TKE) clusters. TKE provides the block storage StorageClass by default. You can use both StorageClass and PersistentVolumeClaim to dynamically create required storage resources.

This document describes how to create a StorageClass of the Cloud File Storage (CFS) type by using the console and Kubectl as well as how to customize the template required by CFS disks.



## Preparations
### Installing the CFS add-on
>? If your cluster has been installed with the CFS-CSI add-on, skip this step.

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. Click **Cluster** in the left sidebar to go to the **Cluster Management** page.
3. Click the ID of the cluster for which you want to create an add-on to go to the **Cluster Details** page.
4. On the "Cluster Details" page, choose **Add-On Management** > **Create** to go to the **Create Add-on** page.
5. On the **Create Add-on** page, select **CFS** and click **Done**.



### Creating a subnet
When creating a StorageClass, you need to set the subnet of CFS. To ensure that all availability zones have suitable subnets in the VPC where the CFS resides, we recommend that you create subnets in advance.

1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1) and click **Subnet** in the left sidebar.
2. On the **Subnet** page, click **+New**. The **Create a Subnet** page appears, where you can configure the Subnet Name, VPC IP Range, CIDR, Availability Zone, and associated route table, as shown in the following figure.
![](https://main.qcloudimg.com/raw/f95414e493602e4b423e44a15ddc139e.png)
3. (Optional) Click **+Add a line** to create multiple subnets at a time.
4. Click **Create**.

### Creating a permission group and adding permission group rules
When creating a StorageClass, you need to configure a permission group for CFS. To ensure that CFS has a suitable permission group, we recommend that you create a permission group in advance.

1. Log in to the [CFS console](https://console.cloud.tencent.com/cfs) and click **Permission Group** in the left sidebar.
2. On the **Permission Group** page, click **Create**. In the **Create Permission Group** window that appears, configure the permission group name and remarks.
3. Click **Confirm** to create the permission group. It will now appear on the **Permission Group** page.
4. Click the ID of this permission group to go to its details page, where you can add, modify, or delete permission group rules. If no rules have been added to this permission group, all operations are allowed. For more information, see [Creating a permission group rule](https://intl.cloud.tencent.com/document/product/582/10951).


## Directions
### Console operation instructions
<span id="create"></span>
#### Creating a StorageClass via the console
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cluster** in the left sidebar.
2. On the **Cluster Management** page, click the ID of the target cluster to go to the cluster details page.
3. Choose **Storage** > **StorageClass** in the left sidebar to go to the **StorageClass** page, as shown in the following figure.
![](https://main.qcloudimg.com/raw/67c2d9b13758cb8c8b7080ec7b236afc.png)
4. Click **Create** to go to the **Create StorageClass** page, where you can set the parameters as required, as shown in the following figure.
![](https://main.qcloudimg.com/raw/b457e1fed71474e3edc4f282da80487f.png)
Main parameters are described as follows:
	- **Name**: set a custom name. This document uses `cfs-storageclass`as an example.
	- **Provisioner**: select **Cloud File Storage**.
	- **Availability Zone**: set the available zones that can use CFS in the current region. Different regions may support different storage classes in different availability zones. For more information, see [Available Regions](https://intl.cloud.tencent.com/document/product/582/35772).
	- **CFS Subnet**: set the subnet range that can be used by CFS in the current availability zone based on your needs.
	- **Storage Type**: CFS provides **Standard Storage** and **High-Performance Storage**. Different regions may support different storage types in different availability zones. Select a storage type as prompted by the console.
		- **Standard Storage**: this class features low cost and large capacity and is suitable for applications that are cost-sensitive and need large capacity. For example, standard storage can be used for data backup, file sharing, and log storage.
		- **High-Performance Storage**: this class features high throughput and high IOPS and is suitable for I/O-intensive workloads. For example, high-performance storage can be used for high-performance computing, media asset rendering, machine learning, DevOps, and office OA.
	- **File Service Protocol**: NFS is used by default, which allows transparent access to files and file systems on the file server.
	- **Permission Group**: configure a permission group for the file system, which is used to manage the access and read/write permissions of clients that access the file system in the same network. Select an appropriate permission group as required. If no such permission group is available, create one on the [Permission Group](https://console.cloud.tencent.com/cfs/permission) page.
	- **Reclaim Policy**: the reclaim policy for CBS disks. The **Delete** and **Retain** reclaim policies are provided. For data security, we recommend that you select **Retain**.
5. Click **Create StorageClass** to complete the process.

<span id="createPVC"></span>
#### Creating a PVC by using a specified StorageClass
1. On the **Cluster Management** page, select the ID of the cluster for which a PVC needs to be created.
2. On the cluster details page, choose **Storage** > **PersistentVolumeClaim** in the left sidebar to go to the **PersistentVolumeClaim** page, as shown in the following figure.
![](https://main.qcloudimg.com/raw/32c83af0e9ca2fe663993bddc9bbe1e1.png)
3. Click **Create** to go to the **Create PersistentVolumeClaim** page, where you can set key PVC parameters as required, as shown in the following figure.
![](https://main.qcloudimg.com/raw/044c043388d7920b6aef791d673b07d9.png)
Main parameters are described as follows:
- **Name**: set a custom name. This document uses `cfs-pvc` as an example.
- **Namespace**: select **default**.
- **Provisioner**: select **Cloud File Storage**.
- **R/W permission**: CFS only supports multi-server read and write.
- **StorageClass**: specify a StorageClass as required. This document uses the `cfs-storageclass` created in the step of [Creating a StorageClass](#create) as an example.
 >? 
 >- The PVC and PV will be bound to the same StorageClass.
>- If you do not specify a StorageClass, the value of `StorageClass` for the corresponding PVC is empty, and the value of the `storageClassName` field in the corresponding YAML file is a null string.

- **PersistVolume**: specify a PersistentVolume as required. In the example in this document, no PersistentVolume is specified.
>? 
>- The system first searches the current cluster to see whether there are PVs that meet the binding rules. If not, the system dynamically creates a PV to be bound based on the PVC and the selected StorageClass.
>- Either `StorageClass` or `PersistVolume` should be specified.
>- No PersistVolume is specified. For more information, see [PV and PVC binding rules](https://intl.cloud.tencent.com/document/product/457/37770).

4. Click **Create PersistentVolumeClaim** to complete the creation process.

#### Creating a workload to use a PVC volume
>? This step creates a Deployment workload as an example.

1. On the **Cluster Management** page, select the target cluster ID to go to the **Deployment** page of the cluster for which the workload needs to be deployed.
2. Click **Create** to go to the **Create Workload** page. For more information on how to create a workload, see [Creating a Deployment](https://intl.cloud.tencent.com/document/product/457/30662). Then, mount a volume as required, as shown in the following figure.
![](https://main.qcloudimg.com/raw/0ff71649814009bd943042745858275e.png)
	- **Volume (optional)**:
		- **Mount method**: select **Use existing PVC**.
		- **Volume name**: set a custom name. This document uses `cfs-vol` as an example.
		- **Select PVC**: select `cfs-pvc`, which you created in the step of [Creating a PVC](#createPVC2).
	- **Containers in the pod**: click **Add Mount Point** to set a mount point.
       - **Volume**: select the volume `cfs-vol` that you added in this step.
       - **Destination Path**: enter a destination path. This document uses `/cache` as an example.
       - **Sub-path**: mount only a sub-path or a single file in the selected volume, such as `/data` or `/test.txt`.
3. Click **Create Workload** to complete the creation process.
> ! If you use the PVC mount method of CFS, the volume can be mounted to multiple nodes.



### Kubectl operation instructions

You can also create a StorageClass by directly using Kubectl. The template is as follows:
```yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name:  CFS auto
parameters:
# first you must modify vpcid and subnetid in storageclass parameters
  vpcid: vpc-xxxxxxxx
  subnetid: subnet-xxxxxxxx
provisioner: com.tencent.cloud.csi. CFS 
```
The following parameters are supported:
<table>
<tr>
<th>Parameter</th> <th>Optional</th> <th>Description</th>
</tr>
<tr> 
<td>vpcid</td> <td>Yes</td> <td>ID of the VPC where the target CFS resides.</td>
</tr>
<tr> 
<td>subnetid</td> <td>Yes</td> <td>ID of the subnet where the target CFS resides.</td>
</tr>
<tr> 
<td>zone</td> <td>No</td> <td>Region where the target CFS resides.</td>
</tr>
<tr> 
<td>pgroupid</td> <td>No</td> <td>Permission group to which the target CFS belongs.</td>
</tr>
<tr> 
<td>storagetype</td> <td>No</td> <td>Storage type. It is standard storage (SD) by default. Valid values are described as follows:
<ul class="params">
<li>SD: standard storage.</li>
<li>HP: high-performance storage</li>
</ul></td>
</tr>
</table>

<style>
	.params{margin:0px !important}
</style>
