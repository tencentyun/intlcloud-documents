## Overview

A cluster admin can use StorageClass to define different storage classes for Tencent Kubernetes Engine (TKE) clusters. TKE provides the block storage StorageClass by default. You can use both StorageClass and PersistentVolumeClaim to dynamically create required storage resources.

This document describes how to create a StorageClass of the Cloud Block Storage (CBS) type by using the console and Kubectl, and how to customize the template required by CBS disks.

## Directions
### Console operation instructions
<span id="create"></span>
#### Creating a StorageClass
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cluster** in the left sidebar.
2. Click the ID of the cluster for which a StorageClass needs to be created to go to the cluster details page.
3. Select **Storage** > **StorageClass** in the left sidebar to go to the **StorageClass** page, as shown in the following figure.
![](https://main.qcloudimg.com/raw/9c08551ba5e4fe254cebf30eb34a01e1.png)
4. Click **Create** to go to the **Create StorageClass** page, where you can set the parameters as required, as shown in the following figure.
![](https://main.qcloudimg.com/raw/f0a35d376991444679f3cd7dbb79b434.png)
Main parameters are described as follows:
	- **Name**: set a custom name. This document uses `cbs-test` as an example.
	- **Provisioner**: select **Cloud Block Storage**.
	- **Region**: the region where current cluster is located.
	- **Availability Zone**: select the availability zones that support CBS disks in the current region as required.
	- **Billing mode**: the elastic **pay-as-you-go** billing mode is provided. It allows you to enable and terminate instances at any time. The instances are billed based on actual usage, and the delete and retain reclaim policies are supported.
- **Disk Type**: **Premium Cloud Disk**, **SSD Cloud Disk**, and **HSSD Cloud Disk** are supported. Different availability zones may have different disk types. For more information, see [Cloud Disk Types](https://intl.cloud.tencent.com/document/product/213/33000). Select a disk type as prompted by the console.
- **Reclaim Policy**: the reclaim policy for cloud disks. Generally, the **Delete** and **Retain** reclaim policies are provided, which depends on the selected billing mode. For data security, we recommend that you select **Retain**.
- **Volume Binding Mode**: two modes are available: **Bind Now** and **Wait for Scheduling**. Different modes support different volume binding policies. Refer to the following information to select the appropriate mode:
	- **Bind Now**: PVCs created via the storageclass will be directly bound with the PV and allocated.
	- **Wait for Scheduling**: PVCs created via the storageclass will not be bound with the PV and allocated until the pod that uses the PVCs is created.
- **Scheduled Snapshot**: setting scheduled snapshot policy can effectively protect data security, but data backup will generate certain fees. For more information, see [Snapshot Overview](https://intl.cloud.tencent.com/document/product/362/31638).

	>? The default-policy configuration provided by TKE for backup includes the date of backup execution, time point of backup execution, and backup retention period.
	
5. Click **Create a StorageClass** to complete the process.

   <span id="createPVC"></span>

#### Creating a PVC by using a specified StorageClass
1. On the **Cluster Management** page, select the ID of the cluster for which a PVC needs to be created.
2. On the cluster details page, choose **Storage** > **PersistentVolumeClaim** in the left sidebar to go to the **PersistentVolumeClaim** page, as shown in the following figure.
![](https://main.qcloudimg.com/raw/1ebfd35584e86e4ca050c03ffc0a979c.png)
3. Click **Create** to go to the **Create a PersistentVolumeClaim** page, where you can set key PVC parameters as required, as shown in the following figure.
![](https://main.qcloudimg.com/raw/1654bb4dbce684a4492f3f155159f2b7.png)
Main parameters are described as follows:
   - **Name**: set a custom name. This document uses `cbs-pvc` as an example.
   - **Namespace**: select **default**.
   - **Provisioner**: select **CBS**.
   - **R/W permission**: CBS disks only support **Single machine read and write**.
   - **StorageClass**: specify a StorageClass as required. This document uses the `cbs-test` created in the step of [Creating a StorageClass](#create) as an example.
>?
>- The PVC and PV will be bound to the same StorageClass.
>- If you do not specify a StorageClass, the value of `StorageClass` for the corresponding PVC is empty, and the value of the `storageClassName` field in the corresponding YAML file is a null string.

   - **PersistVolume**: specify a PersistentVolume as required. In the example in this document, no PersistentVolume is specified.
>? 
>- The system first searches the current cluster to see whether there are PVs that meet the binding rules. If no, the system dynamically creates a PV to be bound based on the PVC and the selected StorageClass.
>- If `StorageClass` is not specified, then `PersistVolume` must be specified.
>- No PersistentVolume is specified. For more information, see [PV and PVC Binding Rules](https://intl.cloud.tencent.com/document/product/457/37770).

   **Disk Type**: based on the selected StorageClass, the available disk types are displayed: **Premium Cloud Disk**, **SSD Cloud Disk** and **Enhanced SSD Cloud Disk**.
   - **Capacity**: if no PersistentVolume is specified, specify the expected cloud disk capacity.
   - **Cost**: based on the above parameters, calculate the cost of the corresponding cloud disk. For more information, see [Billing Modes](https://intl.cloud.tencent.com/document/product/362/32415).
4. Click **Create a PersistentVolumeClaim** to complete the creation.

#### Creating a StatefulSet to mount a PVC volume
>? This step creates a StatefulSet workload as an example.

1. On the details page of the target cluster, choose **Workload** > **StatefulSet** in the left sidebar to go to the **StatefulSet** page.
2. Click **Create** to go to the **Create Workload** page. For more information, see [Creating a StatefulSet](https://intl.cloud.tencent.com/document/product/457/30663). Then, mount a volume as required, as shown in the following figure.
![](https://main.qcloudimg.com/raw/9574b60607fc80b0226136ca13f6fbdb.png)
	- **Volume (optional)**:
		- **Mount method**: select **Use existing PVC**.
		- **Volume name**: set a custom name. This document uses `cbs-vol`as an example.
		- **Select PVC**: select an existing PVC. This document uses the `cbs-pvc`, which you created in the step of [Creating a PVC by using a specified StorageClass](#createPVC), as an example.
	- **Containers in the pod**: click **Add Mount Point** to set a mount point.
		- **Volume**: select the volume `cbs-vol` that you added in this step.
		- **Destination Path**: enter a destination path. This document uses `/cache` as an example.
		- **Sub-path**: mount only a sub-path or a single file in the selected volume, such as `/data` or `/test.txt`.
3. Click **Create Workload** to complete the process.

>! If you use the PVC mount method of CBS, the volume can be mounted to only one node.


### Kubectl operation instructions
You can use the sample template in this document to create a StorageClass by using Kubectl.


#### Creating a StorageClass
The following sample YAML file is used to create a StorageClass with the default name of cbs in a cluster.
```yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  # annotations:
  #   storageclass.beta.kubernetes.io/is-default-class: "true"
  # If this line is present, it will become the default-class, and if you do not specify a type when creating a PVC, this type will be used automatically.
  name: cloud-premium
provisioner: cloud.tencent.com/qcloud-cbs ## The provisioner coming with the TKE cluster
parameters:
  type: CLOUD_PREMIUM
  # CLOUD_PREMIUM, CLOUD_SSD and CLOUD_HSSD are supported. If it is not recognized, CLOUD_PREMIUM is used by default.
  # renewflag: NOTIFY_AND_AUTO_RENEW
  # renewflag indicates the CBS renewal mode. NOTIFY_AND_AUTO_RENEW supports notifications upon expiration and automatic renewal by month. NOTIFY_AND_MANUAL_RENEW supports notifications upon expiration and but not automatic renewal. DISABLE_NOTIFY_AND_MANUAL_RENEW does not support notifications upon expiration or automatic renewal. If not specified, NOTIFY_AND_MANUAL_RENEW is used by default.
  # paymode: PREPAID
  - paymode: the billing method of the cloud disk. The default value is POSTPAID (pay-as-you-go, which supports the **Retain** and **Delete** reclaim policies. **Retain** is only available in cluster version 1.8 or later).
  # aspid:asp-123
  # You can specify a snapshot policy. After the cloud disk is created, it will be automatically bound to this policy. Binding failure does not affect the creation.
```
The following table lists the supported parameters.
<table>
<tr>
<th>Parameter</th> <th>Description</th>
</tr>
<tr>
<td>type</td> <td>Cloud disk types, which can be <code>CLOUD_HSSD</code>, <code>CLOUD_PREMIUM</code> and <code>CLOUD_SSD</code>.</td>
</tr>
<tr>
<td>zone</td> <td>Availability zone. If an availability zone is specified, the cloud disk is created in this availability zone. If no availability zone is specified, the availability zones of all nodes are obtained and one is selected at random. For the identifiers of all Tencent Cloud regions, see <a href="https://intl.cloud.tencent.com/document/product/213/6091">Regions and Availability Zones</a>.</td>
</tr>
<tr>
<td>paymode</td> <td>The billing method of the cloud disk. The default value is <code>POSTPAID</code> (pay-as-you-go), which supports the **Retain** and **Delete** reclaim policies. **Retain** is only available in clusters later than V1.8.</td>
</tr>
<tr>
<td>renewflag</td> <td>CBS renewl mode. The default value is <code>NOTIFY_AND_MANUAL_RENEW</code>.<ul><li><code>NOTIFY_AND_AUTO_RENEW</code> indicates that the created CBS supports notifications upon expiration and automatic renewal by month.</li><li><code>NOTIFY_AND_MANUAL_RENEW</code> indicates that the created CBS supports notifications upon expiration but not automatic renewal.</li><li> <code>DISABLE_NOTIFY_AND_MANUAL_RENEW</code> indicates that the created CBS does not support notifications upon expiration or automatic renewal.</li></ul></td>
</tr>
<tr>
<td>aspid</td> <td>Snapshot policy ID. The created cloud disk will be automatically bound with this policy. Binding failure does not affect the creation of the cloud disk.</td>
</tr>
</table>


#### Creating a multi-pod StatefulSet

You can use a cloud disk to create a multi-pod StatefulSet. The sample YAML file is as follows:

<dx-alert infotype="explain" title="">
The apiVersion of the resource object varies based on the cluster Kubernetes version. You can run the command `kubectl api-versions` to view the apiVersion of the current resource object.
</dx-alert>

``` yaml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: web
spec:
  serviceName: "nginx"
  replicas: 3
  template:
    metadata:
      labels:
        app: nginx
    spec:
      terminationGracePeriodSeconds: 10
      containers:
      - name: nginx
        image: nginx
        ports:
        - containerPort: 80
          name: web
        volumeMounts:
        - name: www
          mountPath: /usr/share/nginx/html
  volumeClaimTemplates: # the system automatically creates a PVC and then automatically creates a PV.
  - metadata:
      name: www
    spec:
      accessModes: [ "ReadWriteOnce" ]
      storageClassName: cloud-premium
      resources:
        requests:
          storage: 10Gi
```
