## Overview
Tencent Kubernetes Engine (TKE) allows you to create persistent volumes (PVs) and persistent volume claims (PVCs) and use existing PVCs when creating workloads and adding volumes so that you can manage CBS disks by using the PVs and PVCs.
>!
>- CBS disks cannot be mounted across availability zones. If a pod with a CBS-type PV mounted is migrated to another availability zone, the mounting relationship will be invalid.
>- The TKE console does not support CBS disk expansion. You can go to the [Cloud Block Storage console](https://console.cloud.tencent.com/cvm/cbs/index) to expand CBS disks. For more information, see [Expanding Cloud Disks](https://intl.cloud.tencent.com/document/product/362/5747).
>






## Operation Directions

### Console operation instructions

<span id="create"></span>

#### Creating a StorageClass via the console

To statically create a PV of the CBS type, you need to bind an available StorageClass of the same type. For more information, see [Creating a StorageClass](https://intl.cloud.tencent.com/document/product/457/36158).

<span id="pv"></span>

#### Creating a PV statically

>? Creating a PV statically is suitable for scenarios where there’re already existing cloud disks used in the cluster.
>
1. Log in to the TKE console and click **[Cluster](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. On the **Cluster Management** page, select the ID of the cluster where the PV needs to be created. The cluster management page of the PV to be created appears.
3. Choose **Storage** -> **PersistentVolume** in the left sidebar. The **PersistentVolume** page appears, as shown in the following figure.
![](https://main.qcloudimg.com/raw/a2b697084a60326eab70b21744f06b36.png)
4. Click **Create** to go to the **Create a PersistentVolume** page, where you can set PV parameters as required, as shown in the following figure.
![](https://main.qcloudimg.com/raw/54d23b15b99b16c503a2ad9f77a2bd57.png)
Main parameters are described as follows:
   - **Creation Method**: select **Manual**.
   - **Name**: set a custom name. This document uses `cbs-pv` as an example.
   - **Provisioner**: select **CBS**.
   - **R/W permission**: CBS disks only support **Single machine read and write**.
   - **StorageClass**: select a StorageClass as required. This document uses `cbs-test`, which you created in the step of [Creating a StorageClass via the console](#create), as an example.
>?
>- The PVC and PV will be bound to the same StorageClass.
>- If you do not specify a StorageClass, the value of `StorageClass` for the corresponding PV is empty, and the value of the `storageClassName` field in the corresponding YAML file is a null string.
   - **Cloud Disk**: select a created cloud disk.
   - **File System**: the default value is ext4.
5. Click **Create a PersistentVolume**.

<span id="createPVC2"></span>

#### Creating a PVC
1. On the details page of the target cluster, choose **Storage** -> **PersistentVolumeClaim** in the left sidebar to go to the **PersistentVolumeClaim** page, as shown in the following figure.
![](https://main.qcloudimg.com/raw/d1848187f200542fe03cb71420cd3837.png)
2. Click **Create** to go to the **Create a PersistentVolumeClaim** page, where you can set PVC parameters as required, as shown in the following figure.

Main parameters are described as follows:
   - **Name**: set a custom name. This document uses `cbs-pvc` as an example.
   - **Namespace**: select **default**.
   - **Provisioner**: select **Cloud Block Storage**.
   - **R/W permission**: CBS disks only support **Single machine read and write**.
   - **StorageClass**: select a StorageClass as required. This document uses `cbs-test`, which you created in the step of [Creating a StorageClass via the console](#create), as an example.
>? 
>- The PVC and PV will be bound to the same StorageClass.
>- If you do not specify a StorageClass, the value of `StorageClass` for the corresponding PVC is empty, and the value of the `storageClassName` field in the corresponding YAML file is a null string.
> 
   - **PersistVolume**: specify a PersistentVolume as required. This document uses use the `cbs-pv` created in the [Creating a PV statically](#pv) step as an example.
>? 
>- Only PVs in the specified StorageClass and in the Available or Released statuses can be selected. If no PV in the current cluster meets the conditions, select **Do not specify** in **Specify PersistVolume**.
>- If the status of the selected PV is Released, you need to manually delete the `claimRef` field in the corresponding YAML configuration file of the PV so that the PV can be successfully bound with the PVC. For more information, see [Rules for Binding PVs and PVCs](https://intl.cloud.tencent.com/document/product/457/37770).
3. Click **Create a PersistentVolumeClaim** to complete the creation.


#### Creating a workload to use a PVC volume
>? This step creates a Deployment workload as an example.
>
1. On the **Cluster Management** page, select the target cluster ID to go to the **Deployment** page of the cluster for which the workload needs to be deployed.
2. Click **Create** to go to the **Create Workload** page. For more information on how to create a workload, see [Creating a Deployment](https://intl.cloud.tencent.com/document/product/457/30662). Then, mount a volume as required, as shown in the following figure.
![](https://main.qcloudimg.com/raw/9205fe5c879dc5755e02f3e5830fc3ba.png)
	- **Volume (optional)**:
		- **Mount method**: select **Use existing PVC**.
		- **Volume name**: set a custom name. This document uses `cbs-vol` as an example.
		- **Select PVC**: select `cfs-pvc`, which you created in the step of [Creating a PVC](#createPVC2).
	- **Containers in the pod**: click **Add Mount Point** to set a mount point.
       - **Volume**: select the volume `cbs-vol` that you added in this step.
       - **Destination Path**: enter a destination path. This document uses `/cache` as an example.
       - **Sub-path**: mount only a sub-path or a single file in the selected volume, such as `/data` or `/test.txt`.
4. Click **Create Workload** to complete the process.
 >! If you use the PVC mount method, the volume can be mounted to only one node.

### Kubectl operation instructions

You can use the following sample YAML file to perform creation by using Kubectl.

<span id="createPV"></span>

#### (Optional) Creating a PV

You can create a PV by using an existing CBS disk, or directly [create a PVC](#createPVC). The system automatically creates the PV. The sample YAML file is as follows:
```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
   name: nginx-pv
"spec":
   capacity:
     storage: 10Gi
   accessModes:
     - ReadWriteOnce
   qcloudCbs:
       cbsDiskId: disk-xxxxxxx ## Specify an existing CBS ID
       fsType: ext4
   storageClassName: cbs
```

<span id="createPVC"></span>

#### Creating a PVC

If you did not [create a PV](#createPV), the system automatically creates the corresponding PV when creating a PVC. The sample YAML file is as follows:
```yaml
kind: PersistentVolumeClaim
apiVersion: v1
metadata:
   name: nginx-pv-claim
"spec":
   storageClassName: cbs
   accessModes:
     - ReadWriteOnce
   resources:
     requests:
       storage: 10Gi
```
- The capacity of an HDD cloud disk must be a multiple of 10, with a minimum of 10 GB.
- The minimum capacity of a premium cloud storage disk is 50 GB.
- The minimum capacity of an SSD disk is 100 GB.

#### Using a PVC

You can create a workload to use a PVC volume. The sample YAML file is as follows:
```yaml
apiVersion: extensions/v1beta1
kind: Deployment
metadata:
   name: nginx-deployment
spec:
   replicas: 1
   selector:
     matchLabels:
       qcloud-app: nginx-deployment
   Template:
     metadata:
       labels:
         qcloud-app: nginx-deployment
     "spec":
       containers:
       - image: nginx
         imagePullPolicy: Always
         name: nginx
         volumeMounts:
         - mountPath: "/opt/"
           name: pvc-test
       volumes:
       - name: pvc-test
         persistentVolumeClaim:
           claimName: nginx-pv-claim # An already created PVC
```
