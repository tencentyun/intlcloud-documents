## Overview
This document guides you through managing cloud disks by using persistent volumes (PVs) and persistent volume claims (PVCs).
>!
>- Tencent Cloud cloud disks cannot be mounted across availability zones. If a pod with a CBS-type PV mounted is migrated to another availability zone, the PV is unmounted automatically.
>- To expand a cloud disk, you need to go to the [Cloud Block Storage console](https://console.cloud.tencent.com/cvm/cbs/index). For more information, see [Expanding Cloud Disks](https://intl.cloud.tencent.com/document/product/362/5747).
>






## Directions

### Operations in TKE console

#### Creating a StorageClass[](id:create)
When you create a CBS PV manually, you need to bind it with a StorageClass of the same type. For more information, see [Creating a StorageClass](https://intl.cloud.tencent.com/document/product/457/36158).


#### Creating a PV manually[](id:pv)
>? This approach is applicable to scenarios where there’re already existing cloud disks used in the cluster.
>
1. Log in to the TKE console and select **[Cluster](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. On the **Cluster Management** page, select the ID of the target cluster. 
3. In the cluster details page, choose **Storage** > **PersistentVolume** in the left sidebar to go to the **PersistentVolume** page, as shown in the following figure.
![](https://main.qcloudimg.com/raw/a2b697084a60326eab70b21744f06b36.png)
4. Click **Create** to go to the **Create PersistentVolume** page and configure the parameters.
   ![](https://main.qcloudimg.com/raw/54d23b15b99b16c503a2ad9f77a2bd57.png)
   The main parameters are described as follows:
   - **Creation Method**: Select **Manual**.
   - **Name**: Set a custom name. This document uses `cbs-pv` as an example.
   - **Provisioner**: Select **Cloud Block Storage**.
   - **R/W permission**: CBS disks only support **Single machine read and write**.
   - **StorageClass**: Select a StorageClass as required. This document uses `cbs-test`, which you created in the [Creating a StorageClass](#create) step, as an example.
>?
>- The PVC and PV are bound to the same StorageClass.
>- If you do not specify a StorageClass, the value of `StorageClass` for the corresponding PV is empty, and the value of the `storageClassName` field in the corresponding YAML file is a null string.
   - **Cloud Disk**: Select an existing cloud disk.
   - **File System**: The default value is ext4.
3. Click **Create a PersistentVolume** to complete the creation.



#### Creating a PVC[](id:createPVC2)
1. On the cluster details page, choose **Storage** > **PersistentVolumeClaim** in the left sidebar to go to the **PersistentVolumeClaim** page, as shown in the following figure.
![](https://main.qcloudimg.com/raw/d1848187f200542fe03cb71420cd3837.png)
2. Click **Create** to go to the **Create PersistentVolumeClaim** page, where you can set PVC parameters as required, as shown in the following figure.
   ![](https://main.qcloudimg.com/raw/ceedef2bd21a5da503098528a2d4900f.png)
   The main parameters are described as follows:
   - **Name**: Set a custom name. This document uses `cbs-pvc` as an example.
   - **Namespace**: Select **default**.
   - **Provisioner**: Select **Cloud Block Storage**.
   - **R/W permission**: CBS disks only support **Single machine read and write**.
   - **StorageClass**: Select a StorageClass as required. This document uses `cbs-test`, which you created in the [Creating a StorageClass](#create) step, as an example.
>? 
>- The PVC and PV are bound to the same StorageClass.
>- If you do not specify a StorageClass, the value of `StorageClass` for the corresponding PVC is empty, and the value of the `storageClassName` field in the corresponding YAML file is a null string.
> 
   - **PersistVolume**: Specify a PersistentVolume. This document uses use the `cbs-pv` created in the [Creating a PV manually](#pv) step as an example.
>? 
>- Only PVs in the specified StorageClass and in the Available or Released statuses can be selected. If no PV in the current cluster meets the conditions, select **Do not specify** in **Specify PersistVolume**.
>- If the status of the selected PV is Released, you need to manually delete the `claimRef` field in the corresponding YAML configuration file of the PV so that the PV can be successfully bound with the PVC. For more information, see [PV and PVC Binding Rules](https://intl.cloud.tencent.com/document/product/457/37770).
3. Click **Create a PersistentVolumeClaim** to complete the creation.


#### Creating a workload to use a PVC volume
>? The following example creates a Deployment workload.
>
1. On the **Cluster Management** page, select the target cluster ID to go to the **Deployment** page.
2. Click **Create** to go to the **Create Workload** page. For more information, see [Creating a Deployment](https://intl.cloud.tencent.com/document/product/457/30662). Then, mount a volume as required, as shown in the following figure.
   ![](https://main.qcloudimg.com/raw/9205fe5c879dc5755e02f3e5830fc3ba.png)
	- **Volume (optional)**:
		- **Mount method**: Select **Use existing PVC**.
		- **Volume name**: Set a custom name. This document uses `cbs-vol` as an example.
		- **Select PVC**: Select `cbs-pvc`, which you created in the step of [Creating a PVC](#createPVC2).
	- **Containers in the Pod**: Click **Add Mount Target** to set a mount target.
       - **Volume**: Select the volume `cbs-vol` that you added in this step.
       - **Destination Path**: Enter a destination path. This document uses `/cache` as an example.
       - **Sub-path**: Mount only a sub-path or a single file in the selected volume, such as `/data` or `/test.txt`.
4. Click **Create Workload** to complete the process.
> ! If you use the PVC mount method of CBS, the volume can be mounted to only one node.

### Kubectl operation instructions

You can use the following sample YAML file to perform creation by using Kubectl.


#### (Optional) Creating a PV[](id:createPV)

You can create a PV by using an existing CBS disk You can also directly [create a PVC](#createPVC) and the a corresponding PV is created automatically. The sample YAML file is as follows:
```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
   name: nginx-pv
spec:
   capacity:
     storage: 10Gi
   accessModes:
     - ReadWriteOnce
   qcloudCbs:
       cbsDiskId: disk-xxxxxxx ## Specify an existing CBS ID
       fsType: ext4
   storageClassName: cbs
```



#### Creating a PVC[](id:createPVC)

If you did not [create a PV](#createPV), the system automatically creates the corresponding PV when creating a PVC. The sample YAML file is as follows:
```yaml
kind: PersistentVolumeClaim
apiVersion: v1
metadata:
   name: nginx-pv-claim
spec:
   storageClassName: cbs
   accessModes:
     - ReadWriteOnce
   resources:
     requests:
       storage: 10Gi
```
- The capacity of the cloud disk must be in whole tens.
- The minimum capacity of a premium cloud disk is 10 GB, and the minimum capacity of an SSD cloud disk or enhanced SSD cloud disk is 20 GB. For details, see the [Creating Cloud Disks](https://intl.cloud.tencent.com/document/product/362/5744).

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
   template:
     metadata:
       labels:
         qcloud-app: nginx-deployment
     spec:
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
