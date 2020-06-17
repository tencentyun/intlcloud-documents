## Introduction
PersistentVolume (PV): cluster storage resource. For example, nodes are resources of a cluster. A PV lifecycle is independent from that of a Pod. You can create different types of PVs depending on the StorageClass type.
PersistentVolumeClaim (PVC): a request to store data. For example, PV is a node resource used by a Pod, and a PVC states that PV resources are used. If PV resources are insufficient, a PVC can create a PV dynamically.



## Considerations

- You cannot mount CBS disks across availability zones. If a Pod with a CBS PV migrates to another availability zone, the mount will fail.
- The TKE console does not support CBS disk scaling. Use the [CBS Console] (https://console.cloud.tencent.com/cvm/cbs/index) to perform such tasks.

## Using PVs and PVCs via the Console

### Creating a static PV
> A static PV is suitable for scenarios where the cloud disk already has data on it and is used in the cluster.
>
1. Log in to the TKE console and select **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. Click the ID of the cluster where PV needs to be created to enter the cluster management page.
3. Select **Storage** > **PersistentVolume** to go to the PersistentVolume information page.
4. Click **Create** to go to the "Create PersistentVolume" page.
5. Set PV parameters as needed. The main parameters are as follows:
   - **Origin**: select **Create a static PV** .
   - **Name**: enter a name.
   - **Provisioner**: select **CBS**.
   - **Read/write permission**: select **Single Read/write**. CBS disks only supports **Single Read/write**.
   - **Select a cloud disk**: select as needed.
   - **StorageClass**: select as needed.
7. Click **Create a PersistentVolume** to complete the creation.



<span id="createPVC2"></span>

### Create PVC

1. Log in to the TKE console and select **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. Select the ID of the cluster where PVC needs to be created to enter the cluster management page.
3. Select **Storage** > **PersistentVolumeClaim** to go to the PersistentVolumeClaim information page.
4. Click **Create** to go to the **Create PersistentVolumeClaim** page.
5. Set PVC parameters as needed. The main parameters are as follows:
   - **Name**: enter a name.
   - **Namespace**: select a namespace type.
   - **Provisioner**: select **CBS**.
   - **Read/write permission**: select **Single read/write**. CBS only supports **Single read/write**.
   - **StorageClass**: select as needed.
   - **Capacity**: set as needed. The minimum capacity of the cloud disk depends on its specification. For more information, refer to [CBS types](https://cloud.tencent.com/product/cbs/types).
6. Click **Create PersistentVolumeClaim** to complete the creation.
> If the existing PVs are insufficient, the system will automatically create a PV.

### Creating a workload using PVC as its data volume
1. Log in to the TKE console and select **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. Click the ID of the cluster where you want to deploy a workload to enter the cluster management page.
3. Under **Workload**, select a workload type to go to the corresponding information page.
4. Click **Create** to go to **Create Workload** page.
5. Set workload name, namespace and other information as instructed. In **Volume**, click **Add Volume**.
6. Select **Use an existing PVC** and enter the name of an existing PVC.
7. Click **Create Workload** to complete the creation.
 > Data volume created by PVC can only mount to one node.

## Using PVs and PVCs via kubectl

PVs and PVCs support CBS and CFS disks. For PVs and PVCs based on CBS, you can use [StorageClass Management](https://intl.cloud.tencent.com/document/product/457/30680) to specify which disk type to bind to a PV. The following is for reference only. You can use kubectl to create PVs and PVCs.



<span id="createPV"></span>.

### (optional) Creating a PV

Create PVs using an existing CBS disk. If there is no PV when [creating a PVC](#createPVC), the system will create one automatically.
```Yaml
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
      cbsDiskId: disk-xxxxxxx ## ID of an existing CBS disk
      fsType: ext4
  storageClassName: cbs
```

<span id="createPVC"></span>

### Creating a PVC

If you have not [created a PV](#createPV), one will be created automatically when the PVC is created. The following is a sample YAML file：
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

- The capacity of a HDD cloud disk must be a multiple of 10, starting at 10 GB.
- The minimum capacity of a Premium Cloud Storage disk is 50 GB.
- The minimum capacity of an SSD cloud disk is 100 GB. For details.

### Using a PVC

The following is a sample YAML file:
```yaml
apiVersion: extensions/v1beta1
kind: Deployment
metadata:
  name: nginx-deployment
"spec":
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
      - image: ng inx
        imagePullPolicy: Always
        name: nginx
        volumeMounts:
        - mountPath: "/opt/"
          name: pvc-test
      volumes:
      - name: pvc-test
        persistentVolumeClaim:
          claimName: nginx-pv-claim # Name of an existing PVC
```
