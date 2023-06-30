## Overview
A cluster admin can use StorageClass to define different storage classes for Tencent Kubernetes Engine (TKE) clusters. TKE provides the block storage StorageClass by default. You can use both StorageClass and PersistentVolumeClaim to dynamically create required storage resources.

This document describes how to create a StorageClass of the Cloud File Storage (CFS) type by using the console and Kubectl as well as how to customize the template required by CFS disks.

## Prerequisites
#### 1. Install the CFS add-on
 If your cluster has been installed with the CFS-CSI add-on, skip this step; otherwise, install it as instructed in [CFS Instructions](https://intl.cloud.tencent.com/document/product/457/36153).




#### 2. Create a subnet
When creating a StorageClass, you need to set the CFS subnet to ensure that every AZ in the CFS's VPC has a suitable subnet. We recommend you create a subnet in advance as instructed in [Creating Subnets](https://intl.cloud.tencent.com/document/product/215/31806). 

#### 3. Create a permission group and add permission group rules
When creating a StorageClass, you need to configure a suitable permission group for the file system. We recommend you create a permission group in advance as instructed in [Managing Permissions](https://intl.cloud.tencent.com/document/product/582/10951).

#### 4. Get the file system FSID
1. In the [CFS console](https://console.cloud.tencent.com/cfs/fs?rid=1), click the ID of the file system for which you want to obtain the FSID. The details page of the file system appears.
2. Select the **Mount target info** tab and get the file system FSID next to **Mount to Linux** such as `a43qadkl` as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/3d1a7cbdcae37e2b4f168a8898203c36.png)
>? For better stability, when you create a PV by YAML and use the NFSv3 protocol for mounting, you need to specify the FSID of the file system to be mounted.


## Console

[](id:create)
### Creating a StorageClass
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and select **Cluster** on the left sidebar.
2. On the **Cluster management** page, click the ID of the target cluster to go to the cluster details page.
3. Select **Storage** > **StorageClass** on the left sidebar.
4. Click **Create** to enter the **Create StorageClass** page, where you can configure StorageClass parameters.
![](https://qcloudimg.tencent-cloud.cn/raw/55d95a4d4f3e1a62dcfce4e8e09039bc.png)
<table>
<thead>
  <tr>
    <th>Configuration Item</th>
    <th>Description</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>Name</td>
    <td>Enter the StorageClass name, for example, `cfs-storageclass`.</td>
  </tr>
	  <tr>   
    <td>Region</td>
    <td>It is the region of the cluster by default. </td>
  </tr>
  <tr>   
    <td>Provisioner</td>
    <td><b>Provisioner</b> can be <b>CBS (CSI)</b> or <b>Cloud File Storage</b>. Here, <b>Cloud File Storage</b> is selected.</td>
  </tr>
  <tr>
    <td>Instance creation mode</td>
    <td>It can be <b>New instance</b> or <b>Shared instance</b>.<ul><li>New instance: During mounting, a CFS instance is created for each PVC by default.</li><li>Shared instance: During mounting, PVCs correspond to different sub-directories of the same CFS instance. The shared CFS instance and its sub-directories are created automatically by the system.</li>
		<dx-alert infotype="explain" title="">The <b>shared instance</b> mode is supported by the CFS-CSI add-on on v1.0.1 or later. Upgrade your add-on in time. Use instructions are as follows:
<li>For a StorageClass in shared instance mode, the <b>Reclaim policy</b> is <b>Retain</b>.</li>
<li>When the StorageClass is used to dynamically create a PVC for the first time, a CFS instance will be created by default, along with its sub-directories to implement isolated mounting of PVCs.</li>
<li>CFS instances created by different StorageClasses in shared instance mode are different. We recommend you limit the number of instances.</li></ul>
</dx-alert></td>
  </tr>
  <tr>
    <td>AZ</td>
    <td>In the current region, select an AZ that supports CFS. Different AZs in the same region support different storage classes. For more information, see <a href="https://intl.cloud.tencent.com/document/product/582/45916">Recommended Regions</a><a href="https://intl.cloud.tencent.com/document/product/582/45916"> </a>.</td>
  </tr>
  <tr>
    <td>CFS subnet</td>
    <td>Set the subnet range of the CFS in the current AZ.</td>
  </tr>
  <tr>
    <td>Storage Type</td>
    <td>CFS provides <b>Standard Storage</b> and <b>Performance Storage</b>. Different AZs in the same region support different storage types. Select one as needed. <ul><li>Standard Storage: It features cost-effectiveness and large capacity, making it suitable for scenarios such as data backup, file sharing, and log storage.</li><li>Performance Storage: It features high throughput and IOPS, making it suitable for IO-intensive workloads such as high-performance computing, media asset rendering, machine learning, DevOps, and OA.</li></ul></td>
  </tr>
  <tr>
    <td>File service protocol</td>
    <td>It is <b>NFS</b> by default to allow for pass-through access to files and file systems on the server.</td>
  </tr>
  <tr>
    <td>Protocol version</td>
    <td>We recommend you use NFSv3 for better performance. If your application relies on file locking (that is, multiple CVM instances are needed to edit a file), use NFSv4 for mounting.</td>
  </tr>
  <tr>
    <td>Permission Group</td>
    <td>Configure a permission group for the file system, which is used to manage the access and read/write permissions of clients that access the file system over the same network. Select a permission group as needed. If no such permission group is available, create one on the <a href="https://console.cloud.tencent.com/cfs/permission">Permission Group</a> page.</td>
  </tr>
  <tr>
    <td>Reclaim policy</td>
    <td>It can be <b>Delete</b> or <b>Retain</b>. The latter is recommended out of data security considerations. <ul><li>Delete: If a PV is dynamically created through a PVC, the PV and storage instance bound to the PVC will be automatically terminated when the PVC is terminated.</li><li>Retain: If a PV is dynamically created through a PVC, the PV and storage instance bound to the PVC will be retained when the PVC is terminated.</li></ul></td>
  </tr>
  <tr>
    <td>Label</td>
    <td>Select the cloud tag to be bound to the CFS instance. The tag will be automatically inherited by the CFS instance that is created dynamically by a StorageClass. After creation, the parameters of the bound tag cannot be modified. If the existing tags are not suitable, create one in the <a href="https://console.cloud.tencent.com/tag/taglist">Tag console</a>.</td>
  </tr>
</tbody>
</table>

5. Click **Create StorageClass** to complete the process.


### Creating a PVC by using the specified StorageClass[](id:createPVC)
1. On the **Cluster management** page, select the ID of the cluster for which a PVC needs to be created.
2. On the cluster details page, select **Storage** > **PersistentVolumeClaim** on the left sidebar.
3. Click **Create** to enter the **Create PersistentVolumeClaim** page, where you can set key PVC parameters.
![](https://main.qcloudimg.com/raw/044c043388d7920b6aef791d673b07d9.png)
<table>
<thead>
  <tr>
    <th>Configuration Item</th>
    <th>Description</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>Name</td>
    <td>Enter the `PersistentVolumeClaim` name, for example, `cfs-pvc`.</td>
  </tr>
  <tr>
    <td>Namespaces</td>
    <td>A namespace is used to assign cluster resources. Here, <b>default</b> is selected.</td>
  </tr>
  <tr>
    <td>Provisioner</td>
    <td>Select <b>Cloud File Storage</b>.</td>
  </tr>
  <tr>
    <td>Read/write permission</td>
    <td>CFS only supports <b>Multi-computer read and write</b>.</td>
  </tr>
  <tr>
    <td>StorageClass</td>
    <td>Specify the StorageClass as needed. Here, <b>Specify</b> is selected. `cfs-storageclass` created in the <a href="https://intl.cloud.tencent.com/document/product/457/36154">Creating a StorageClass</a> step is used as an example.
		<dx-alert infotype="explain" title="">
<ul><li>The PVC and PV will be bound to the same StorageClass.</li>
<li>If you select <b>Do not specify</b>, the value of `StorageClass` for the corresponding PVC is null, and the value of the `storageClassName` field in the corresponding YAML file is a null string.</li></ul>
</dx-alert>
		</td>
  </tr>
  <tr>
    <td>PersistentVolume</td>
    <td>Specify the PersistentVolume as needed. Here, <b>Do not specify</b> is selected.
		<dx-alert infotype="explain" title=""><ul>
<li>The system first searches the current cluster for PVs that meet the binding rules. If there are no such PVs, the system dynamically creates a PV to be bound based on the PVC and StorageClass parameters.</li>
<li>Either the StorageClass or PersistVolume should be specified.</li>
<li>For more information on <b>Do not specify</b> for <b>PersistentVolume</b>, see <a href="https://intl.cloud.tencent.com/document/product/457/37770">PV and PVC binding rules</a>.</li></ul>
</dx-alert>
</td>
  </tr>
</tbody>
</table>

4. Click **Create PersistentVolumeClaim**.

### Creating a workload to use a PVC volume
>? This step creates a Deployment workload as an example.
>
1. On the **Cluster management** page, select the target cluster ID to go to the **Deployment** page of the cluster for which the workload needs to be deployed.
2. Click **Create** to enter the **Create Workload** page. For detailed directions, see [Deployment Management](https://intl.cloud.tencent.com/document/product/457/30662). Then, mount a volume based on the following information.
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

## kubectl

### Creating a StorageClass
```yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: cfs
parameters:
  # subdir-share: "true" 
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
|---------|---------|---------|
| zone | No | It defines the region for the CFS instance. |
| pgroupid | No | It defines the permission group for the CFS instance. |
|storagetype| No | It defaults to Standard Storage (SD). Valid values: <br>SD (Standard Storage)<br>HP (High-Performance Storage). |
|subdir-share|Yes|It indicates the shared instance mode for instance creation by StorageClass.|
| vpcid | Yes | It indicates the ID of the VPC where the file is stored. |
| subnetid | Yes | It indicates the ID of the subnet where the file is stored. |
| vers | Yes | It indicates the version of the protocol used by the add-on to connect to the file system. The dynamically created PVs inherit this parameter. The versions "3" and "4" are supported. |
| resourcetags | Yes | It indicates the cloud tag of the file system. A corresponding Tencent Cloud tag is applied on the generated file system. Multiple tags are separated by comma. For example, "a:b,c:d". |

### Creating a PVC
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
  volumeName: XXX  # You don't need to specify it for dynamic creation. For static creation, you need to specify the PV instance ID. 
```

| Parameter | Required | Description |
| -- | -- | -- |
| spec.accessModes | No | The cfs storage supports Multiple-Read-Multiple-Write. |
| spec.resources.requests.storage | Yes | The storage capacity only depends on the type of the file system. |
>? 
> 1. CFS supports expanding the storage capacity of the file system according to the file size. The requests and applications are not interrupted during the expansion. The default CFS instance capacity is 10 GiB, and the upper limit of the capacity depends on the product type. For details, see [System Restrictions](https://intl.cloud.tencent.com/document/product/582/9135).
> 2. The PVs dynamically created through a PVC inherit the parameters configured in StorageClass. The parameters are generated automatically by the storage add-on.

