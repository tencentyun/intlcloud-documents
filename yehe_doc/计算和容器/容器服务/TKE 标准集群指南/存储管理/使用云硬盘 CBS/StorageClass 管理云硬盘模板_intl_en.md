A cluster admin can use StorageClass to define different storage classes for Tencent Kubernetes Engine (TKE) clusters. TKE provides the block storage StorageClass by default. You can use both StorageClass and PersistentVolumeClaim to dynamically create required storage resources. This document describes how to create a StorageClass of the Cloud Block Storage (CBS) type by using the console and Kubectl, and how to customize the template required by CBS disks.


## Console Operation Directions

### Creating StorageClass[](id:create)
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cluster** in the left sidebar.
2. Click the ID of the cluster for which a StorageClass needs to be created to go to the cluster details page.
3. Click **Storage** > **StorageClass** in the left sidebar, as shown in the following figure.
![](https://main.qcloudimg.com/raw/9c08551ba5e4fe254cebf30eb34a01e1.png)
4. Click **Create** to go to the **Create StorageClass** page, where you can set the parameters as required, as shown in the following figure.
![](https://main.qcloudimg.com/raw/f0a35d376991444679f3cd7dbb79b434.png)
The main parameters are described as follows:
	- **Name**: Set a custom name. This document uses `cbs-test` as an example.
	- **Region**: The region where the current cluster is located.
	- **Provisioner**: Select **Cloud Block Storage (CSI)**.
	- **Availability zone**: Select the availability zones that support CBS disks in the current region as required.
	- **Billing mode**: The **pay-as-you-go** billing mode is provided. It allows you to enable and terminate instances at any time. The instances are billed based on actual usage, and the **Delete** and **Retain** reclaim policies are supported.
	- **Disk type**: **Premium Cloud Disk**, **SSD Cloud Disk**, **Enhanced SSD Cloud Disk**, and **Balanced SSD** are supported. Different availability zones may have different disk types. For more information, see [Cloud Disk Types](https://intl.cloud.tencent.com/document/product/213/33000). Select a disk type as prompted by the console.
	- **Volume binding mode**: The modes of **Bind now** and **Wait for scheduling** are available. Different modes support different volume binding policies. Refer to the following information to select the appropriate mode:
		- **Bind now**: PVCs created via the storageclass will be directly bound with the PV and allocated.
		- **Wait for scheduling**: PVCs created via the storageclass will not be bound with the PV and allocated until the pod that uses the PVCs is created.
	- **Scheduled snapshot**: Setting scheduled snapshot policy can effectively protect data security, but data backup will generate certain fees. For more information, see [Snapshot Overview](https://intl.cloud.tencent.com/document/product/362/31638).
>? The default-policy configuration provided by TKE for backup includes the date of backup execution, time point of backup execution, and backup retention period.
>
  - **Online expansion**: Specify whether to enable online expansion. For more information about online expansion, see [Online Expansion of Cloud Disk](https://intl.cloud.tencent.com/document/product/457/45999).
  - **Reclaim policy**: The reclaim policy for cloud disks. Generally, the **Delete** and **Retain** reclaim policies are provided, which depends on the selected billing mode. For data security, we recommend that you select **Retain**.
5. Click **Create a StorageClass** to complete the process.

### Creating a PVC by using a specified StorageClass[](id:createPVC)
1. On the **Cluster management** page, select the ID of the cluster for which a PVC needs to be created.
2. On the cluster details page, choose **Storage** > **PersistentVolumeClaim** in the left sidebar to go to the **PersistentVolumeClaim** page, as shown in the following figure.
![](https://main.qcloudimg.com/raw/1ebfd35584e86e4ca050c03ffc0a979c.png)
3. Click **Create** to go to the **Create a PersistentVolumeClaim** page, where you can set key PVC parameters as required, as shown in the following figure.
![](https://main.qcloudimg.com/raw/1654bb4dbce684a4492f3f155159f2b7.png)
The main parameters are described as follows:
   - **Name**: set a custom name. This document uses `cbs-pvc` as an example.
   - **Namespace**: Select **default**.
   - **Provisioner**: Select **Cloud Block Storage (CSI)**.
   - **R/W permission**: CBS disks only support **Single machine read and write**.
<dx-alert infotype="explain" title="">
- **Single machine read and write**: Currently, CBS disks can only be mounted to the same machine, and therefore, CBS supports only data read and write processing on a single machine.
- **Multi computer read and write**: CFS/COS objects can be mounted to multiple machines, and therefore, CFS/COS supports data read and write processing on multiple machines.
</dx-alert>

    - **StorageClass**: Specify a StorageClass as required. This document uses the `cbs-test` created in the step of [Creating a StorageClass](#create) as an example.
<dx-alert infotype="explain" title="">
- The PVC and PV will be bound to the same StorageClass.
- If you do not specify a StorageClass, the value of `StorageClass` for the corresponding PVC is empty, and the value of the `storageClassName` field in the corresponding YAML file is a null string.
  </dx-alert>

     - **PersistVolume**: Specify a PersistentVolume as required. In the example in this document, no PersistentVolume is specified.

  <dx-alert infotype="explain" title="">
     - The system first searches the current cluster to see whether there are PVs that meet the binding rules. If no, the system dynamically creates a PV to be bound based on the PVC and the selected StorageClass.
     - If `StorageClass` is not specified, then `PersistVolume` must be specified.
     - No PersistentVolume is specified. For more information, see [PV and PVC Binding Rules](https://intl.cloud.tencent.com/document/product/457/37770).
</dx-alert> 
  
     - **Disk type**: Based on the selected StorageClass, the available disk types are displayed: **Premium Cloud Disk**, **SSD Cloud Disk** and **Enhanced SSD Cloud Disk**.
   - **Capacity**: When PersistentVolume is not specified, you need to indicate the desired capacity of the cloud disk. The capacity must be a multiple of 10. For premium cloud disk, the minimum capacity is 10 GB, and for SSD cloud disk and enhance SSD cloud disk, the minimum capacity is 20 GB.
   - **Cost**: Based on the above parameters, calculate the cost of the corresponding cloud disk. For more information, see [Billing Modes](https://intl.cloud.tencent.com/document/product/362/32415).
4. Click **Create a PersistentVolumeClaim** to complete the creation.

### Creating a StatefulSet to mount a PVC volume
>? This step creates a StatefulSet workload as an example.
>
1. On the details page of the desired cluster, choose **Workload** > **StatefulSet** in the left sidebar to go to the **StatefulSet** page.
2. Click **Create** to go to the **Create Workload** page. For more information, see [Creating a StatefulSet](https://intl.cloud.tencent.com/document/product/457/30663). Then, mount a volume as required, as shown in the following figure.
![](https://main.qcloudimg.com/raw/9574b60607fc80b0226136ca13f6fbdb.png)
	- **Volume (optional)**:
		- **Mount method**: Select **Use existing PVC**.
		- **Volume name**: Set a custom name. This document uses `cbs-vol` as an example.
		- **Select PVC**: Select an existing PVC. This document uses the `cbs-pvc`, which you created in the step of [Creating a PVC by using a specified StorageClass](#createPVC), as an example.
	- **Containers in the Pod**: Click **Add mount target** to set a mount target.
		- **Volume**: Select the volume `cbs-vol` that you added in this step.
		- **Destination path**: Enter a destination path. This document uses `/cache` as an example.
		- **Sub-path**: Mount only a sub-path or a single file in the selected volume, such as `/data` or `/test.txt`.
4. Click **Create Workload** to complete the process.
>! If you use the PVC mount method of CBS, the volume can be mounted to only one node.

## Kubectl Operation Directions
You can use the sample template in this document to create a StorageClass by using Kubectl.


### Creating a StorageClass
The following sample YAML file is used to create a StorageClass with the default name of cbs in a cluster.
```yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  # annotations:
  #   storageclass.beta.kubernetes.io/is-default-class: "true"
  # If this line is present, it will become the default-class, and if you do not specify a type when creating a PVC, this type will be used automatically.
   name: cloud-premium

# If the CBS-CSI add-on is installed for the TKE cluster, enter `com.tencent.cloud.csi.cbs` for `provisioner`.
# If the CBS-CSI add-on is not installed, enter `cloud.tencent.com/qcloud-cbs` for `provisioner` (this capability is deprecated in v1.20 and later versions).
provisioner: com.tencent.cloud.csi.cbs 

parameters:
   type: CLOUD_PREMIUM
   renewflag: NOTIFY_AND_AUTO_RENEW
   paymode: POSTPAID_BY_HOUR
   aspid: asp-123
reclaimPolicy: Retain
volumeBindingMode: WaitForFirstConsumer
```
The following table lists the supported parameters.
<table>
<tr>
<th>Parameter</th> <th>Description</th>
</tr>
<tr>
<td>type</td> <td> This includes CLOUD_PREMIUM (Premium cloud disk), CLOUD_SSD (SSD cloud disk) and CLOUD_HSSD (enhanced SSD cloud disk).</td>
</tr>
<tr>
<td>zone</td> <td>Availability zone. If an availability zone is specified, the cloud disk is created in this availability zone. If no availability zone is specified, the availability zones of all nodes are obtained and one is selected at random. For the identifiers of all Tencent Cloud regions, see <a href="https://intl.cloud.tencent.com/document/product/213/6091">Regions and Availability Zones</a>.</td>
</tr>
<tr>
<td>paymode</td> <td>The billing method of the cloud disk. The default value is <code>POSTPAID_BY_HOUR</code> (pay-as-you-go), which supports the **Retain** and **Delete** reclaim policies. **Retain** is only available in clusters later than V1.8.</td>
</tr>
<tr>
<td>volumeBindingMode</td> <td>The volume binding mode. Two modes are supported: **Immediate** (bind now) and **WaitForFirstConsumer** (wait for scheduling).</td>
</tr>
<tr>
<td>reclaimPolicy</td> <td>The reclaim policy. Two policies are supported: **Delete** and **Retain**.</td>
</tr>
<tr>
<td>renewflag</td> <td>CBS renewal mode. The default value is <code>NOTIFY_AND_MANUAL_RENEW</code>.<li><code>NOTIFY_AND_AUTO_RENEW</code> indicates that the created CBS supports notifications upon expiration and automatic renewal by month.</li><li><code>NOTIFY_AND_MANUAL_RENEW</code> indicates that the created CBS supports notifications upon expiration but not automatic renewal.</li><li> <code>DISABLE_NOTIFY_AND_MANUAL_RENEW</code> indicates that the created CBS does not support notifications upon expiration or automatic renewal.</li></td>
</tr>
<tr>
<td>aspid</td> <td>Snapshot policy ID. The created cloud disk will be automatically bound with this policy. Binding failure does not affect the creation of the cloud disk.</td>
</tr>
</table>



### Creating a multi-Pod StatefulSet

You can use a cloud disk to create a multi-pod StatefulSet. The sample YAML file is as follows:
<dx-alert infotype="explain" title="">
The apiVersion of the resource object varies based on the cluster Kubernetes version. You can run the command `kubectl api-versions` to view the apiVersion of the current resource object.
</dx-alert>
```yaml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: web
spec:
  selector:
    matchLabels:
      app: nginx
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
