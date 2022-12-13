## Overview
Tencent Kubernetes Engine (TKE) allows you to use Cloud Object Storage (COS) by creating PersistentVolumes (PVs) or PersistentVolumeClaims (PVCs) and mounting volumes to workloads. This document describes how to mount COS to a workload.

## Preparations
### Installing the COS add-on
>? If your cluster has been installed with the COS-CSI add-on, skip this step.
>
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **Cluster** to go to the **Cluster Management** page.
3. Select the ID of the cluster for which you want to create an add-on and click **Add-On Management** on the left on the cluster details page.
4. On the **Add-On Management** page, click **Create** to enter the **Create Add-on** page.
5. Select **Tencent Cloud COS** and click **Complete**.

### Creating an access key[](id:CreatAccessKey)
>!To avoid loss to your cloud assets due to root account key leakage, we recommend that you disable your root account from logging in to the console, or use the root account key to access cloud APIs but use a sub-account or collaborator with the relevant management permissions to operate related resources. For more information, see [Security Best Practice](https://www.tencentcloud.com/document/product/598/10592).
> 
> This document describes how to create or view an access key by using a sub-user with the relevant access and management permissions. For more information on how to create a sub-user and grant access and management permissions to the sub-user, see [Creating a Custom Sub-user](https://intl.cloud.tencent.com/document/product/598/13674).
> 
1. Use a sub-account to log in to the [Cloud Access Management console](https://console.cloud.tencent.com/cam/overview) and choose **Access Key** -> **API Keys** in the left sidebar to go to the **API Key Management** page.
2. Click **Create Key** and wait until the key is created.
>?
> - One sub-user can have at most two API keys.
> - An API key is an important credential for creating Tencent Cloud API requests. To keep your assets and services secure, store your keys appropriately and change them regularly. Delete old keys when new ones are created.

### Creating a bucket[](id:CreatBucket)
>! According to relevant laws and policies, you need to complete [Identity Verification](https://console.cloud.tencent.com/developer/auth) before using Tencent Cloud COS.
>
1. Log in to the [COS console](https://console.cloud.tencent.com/cos5) and click **Bucket List** in the left sidebar to go to the **Bucket List** page.
2. Click **Create Bucket**. In the **Create Bucket** page that appears, set the parameters as required, as shown in the following figure.
![](https://main.qcloudimg.com/raw/eb8c2ca6089302bd1f3b78bcd9daf6f8.png)
![](https://qcloudimg.tencent-cloud.cn/raw/bb03a85518bc7c01a86ffc4156a684c4.png)
   - **Region**: select the region where the target cluster described in this document resides, which cannot be modified once configured. For more information, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224).
   -**Name**: enter a custom bucket name, which constructed from the [custom name]-[developer’s APPID] and cannot be modified once configured. For naming instructions, see [Naming Conventions](https://intl.intl.cloud.tencent.com/document/product/436/13312).
   - **Access Permission**: a bucket provides three types of access permissions by default, i.e., **Private Read/Write**, **Public Read/Private Write**, and **Public Read/Write**. The configured permission can be modified later.
      - **Private Read/Write**: only the creator of this bucket and authorized accounts have the read/write permissions for objects in this bucket. This is the default access permission for a bucket and is recommended.
      - **Public Read/Private Write**: everyone (including anonymous visitors) has the read permission for objects in this bucket, but only the creator of this bucket and authorized accounts have the write permission for objects in this bucket.
      - **Public Read/Write**: everyone (including anonymous visitors) has the read and write permissions for objects in this bucket. This is not recommended.
   - **Versioning**: this feature allows you to save multiple versions of an object in the same bucket.
   - **Logging**: records logs of bucket-related requests.
   -**Bucket Tag**: the bucket tag is used as a key pair (key = value) and an identifier to manage buckets in groups. For more information, see [Setting Bucket Tags](https://cloud.tencent.com/document/product/436/30928).
   - **Server-Side Encryption**: valid values include **None** and **SSE-COS**, where the latter indicates server-side encryption that uses COS to manage keys.
      - **SSE-COS**: server-side encryption that uses COS to manage keys. COS is used to host the primary key and manage data. You can use COS to directly manage and encrypt data. For more information, see [Server-side Encryption Overview](https://intl.cloud.tencent.com/document/product/436/18145).
3. Verify the information and click **Create**. After the bucket is created, you can find it in the bucket list.

### Getting the bucket subdirectory[](id:getPath)

1. On the **Bucket List** page, select the name of the created bucket to enter its details page.
2. On the bucket details page, select the subfolder to be mounted to enter its details page. Get the subdirectory path `/costest` in the top-right corner of the page as shown below:
![](https://main.qcloudimg.com/raw/abcc4a290bee8163889b2593836d9683.png)

## Directions

### Using COS via the console

#### Creating a Secret that can access COS[](id:StepOne)

1. In the left sidebar, click **Cluster** to go to the **Cluster Management** page.
2. Select the ID of the target cluster to go to the cluster details page.
3. On the cluster details page, choose **Configuration Management** -> **Secret** in the left sidebar to go to the **Secret** page, as shown in the following figure.
![](https://main.qcloudimg.com/raw/92d8c864b36bf486b7e034973396da65.png)
4. Click **Create** to go to the **Create Secret** page, where you can set the parameters as required, as shown in the following figure.
![](https://main.qcloudimg.com/raw/1066fb90d03545ed7ee358a90e0d3ef7.png)
	- **Name**: set a custom name. This document uses `cos-secret` as an example.
	- **Secret Type**: Select **Opaque**. This type is suitable for saving key certificates and configuration files. The value is Base64-coded.
	- **Effective Scope**: select **Specific Namespace**. Make sure that the Secret is created under the `kube-system` namespace.
	- **Content**: this is used to set the access key required by the Secret to access the bucket. It must contain the variable names `SecretId` and `SecretKey` and their corresponding variable values. Refer to [Creating access key](#CreatAccessKey) to create an access key, and go to the [API Key Management](https://console.cloud.tencent.com/cam/capi) page to get its details.
5. Click **Create Secret**.

#### Creating a PV that supports dynamic COS-CSI configuration[](id:StepTwo)
>! This step requires a bucket. If no bucket is available in the current region, create one. For more information, see [Creating a bucket](#CreatBucket).
>
1. On the details page of the target cluster, choose **Storage** > **PersistentVolume** in the left sidebar to go to the **PersistentVolume** page.
2. Click **Create** to go to the **Create PersistentVolume** page and set the PV parameters as required, as shown in the following figure.
![](https://qcloudimg.tencent-cloud.cn/raw/877c3c9fd14584747794edaf95099027.png)
The main parameters are described as follows:
	- **Creation Method**: select **Manual**.
	- **Name**: set a custom name. This document uses `cos-pv` as an example.
	- **Provisioner**: select **COS**.
	- **R/W permission**: COS only supports multi-host read and write.
>?
>- **Single machine read and write**: Currently, CBS disks can only be mounted to the same machine, and therefore, only data read and write on a single machine can be processed.
>- **Multi computer read and write**: CFS/COS can be mounted to multiple machines at a time, and therefore, data read and write on multiple machines can be processed.
>
	- **Secret**: select the Secret created in [step 1](#StepOne). This document uses `cos-secret` as an example (make sure that the Secret is created under the `kube-system` namespace).
	- **Bucket List**: the list of buckets used to save COS objects. You can select an available bucket as required.
	- **Bucket Subdirectory**: enter the bucket subdirectory obtained in [Getting bucket subdirectory](#getPath). This document uses `/costest` as an example. If the entered subdirectory does not exist, the system will automatically create it for you.
	- **Domain**: the default domain name is displayed. You can use this domain name to access the bucket.
	- **Mount Option**: the COSFS tool allows a bucket to be mounted locally. After the bucket is mounted, you can directly operate on the COS objects in it. This option is used to set related restrictions. The mount option `-oensure_diskfree=20480` in this example indicates that when the free space of the disk where the cache files are stored is less than 20,480 MB, the COSFS tool will fail to be started.
>? Different mount options must be separated with spaces. For more mount options, see the [common mount options documentation](https://intl.cloud.tencent.com/document/product/436/6883).
3. Click **Create a PersistentVolume**.

#### Creating a PVC to bind a PV[](id:StepThree)
>! Do not bind a PV that is in the bound state.
>
1. On the details page of the target cluster, choose **Storage** > **PersistentVolumeClaim** in the left sidebar to go to the **PersistentVolumeClaim** page.
2. Click **Create** to go to the **Create a PersistentVolumeClaim** page, where you can set the parameters as required, as shown in the following figure.
![](https://main.qcloudimg.com/raw/5863b8983019a9a40531b750062010c6.png)
	- **Name**: set a custom name. This document uses `cos-pvc` as an example.
	- **Namespace**: select **kube-system**.
	- **Provisioner**: Select **COS**.
	- **R/W permission**: COS only supports multi-host read and write.
	- **PersistentVolume**: select the PV that you created in [Step 2](#StepTwo). This document uses `cos-pv` as an example.
3. Click **Create PersistentVolumeClaim**.

#### Creating a pod that uses a PVC
>? This step creates a Deployment workload as an example.
>
1. On the details page of the target cluster, choose **Workload** -> **Deployment** to go to the **Deployment** page.
2. Click **Create** to go to the **Create Workload** page. For more information, see [Creating a Deployment](https://intl.cloud.tencent.com/document/product/457/30662). Then, mount a volume as required, as shown in the following figure.
![](https://main.qcloudimg.com/raw/c295374ca83c63c1dc5346e2346ba72a.png)
	- **Volume (optional)**:
      - **Mount method**: Select **Use existing PVC**.
      - **Volume name**: set a custom name. This document uses `cos-vol` as an example.
      - **Select PVC**: select the PVC that you created in [Step 3](#StepThree). This document uses `cos-pvc` as an example.
	- **Containers in the Pod**: Click **Add mount target** to set a mount target.
      - **Volume**: select the volume `cos-vol` that you added in this step.
      - **Destination path**: Enter a destination path. This document uses `/cache` as an example.
      - **Sub-path**: mount only a sub-path or a single file in the selected volume, such as `./data` or `data`.
3. Click **Create Workload**.

### Using COS via a YAML file

#### Creating a Secret that can access COS[](id:StepOne)

You can create a secret that can access COS by using a YAML file. The YAML file template is as follows:
```yaml
apiVersion: v1
kind: Secret
type: Opaque
metadata:
   name: cos-secret
   # Replaced by your secret namespace.
   namespace: kube-system
data:
   # Replaced by your temporary secret file content. You can generate a temporary secret key with these docs:
   # Note: the value must be encoded by base64.
   SecretId: VWVEJxRk5Fb0JGbDA4M...(base64 encode)
   SecretKey: Qa3p4ZTVCMFlQek...(base64 encode)
```

#### Creating a PV that supports dynamic COS-CSI configuration[](id:StepTwo)
You can create a PV to support COS-CSI dynamic configuration by using a YAML file. The YAML file template is as follows:
```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: cos-pv
spec:
  accessModes:
  - ReadWriteMany
  capacity:
    storage: 10Gi
  csi:
    driver: com.tencent.cloud.csi.cosfs
    nodePublishSecretRef:
      name: cos-secret
      namespace: kube-system
    volumeAttributes:
      # Replaced by the url of your region.
      url: http://cos.ap-XXX.myqcloud.com
      # Replaced by the bucket name you want to use.
      bucket: XXX-1251707795
      # You can specify sub-directory of bucket in cosfs command in here.
      path: /costest
       # You can specify any other options used by the cosfs command in here.
    # additional_args: "-oallow_other"# Specify a unique volumeHandle like bucket name. (This value must be different from other pv's volumeHandle.)
    volumeHandle: XXX
  persistentVolumeReclaimPolicy: Retain
  volumeMode: Filesystem
```

#### Creating a PVC that binds a PV

You can create a PVC that binds the preceding PV by using a YAML file. The YAMl file template is as follows:
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
   name: cos-pvc
spec:
   accessModes:
   - ReadWriteMany
   resources:
     requests:
       storage: 1Gi
   # You can specify the pv name manually or just let kubernetes to bind the pv and pvc.
   # volumeName: cos-pv
   # Currently cos only supports static provisioning, the StorageClass name should be empty.
   storageClassName: ""
```

#### Creating a pod that uses a PVC
You can create a pod by using a YAML file. The YAML file template is as follows:
```yaml
apiVersion: v1
kind: Pod
metadata:
   name: pod-cos
spec:
   containers:
   - name: pod-cos
     command: ["tail", "-f", "/etc/hosts"]
     image: "centos:latest"
     volumeMounts:
     - mountPath: /data
       name: cos
     resources:
       requests:
         memory: "128Mi"
         cpu: "0.1"
   volumes:
   - name: cos
     persistentVolumeClaim:
       # Replaced by your pvc name.
       claimName: cos-pvc
```

## More Information
For more information on how to use COS, see [README_COSFS.md](https://github.com/TencentCloud/kubernetes-csi-tencentcloud/blob/master/docs/README_COSFS.md).
