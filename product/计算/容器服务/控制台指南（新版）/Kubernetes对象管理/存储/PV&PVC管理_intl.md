## Overview

### Definitions

PersistentVolume (PV): A storage resource within a cluster. For example, a node is a resource of a cluster. A PV is independent of the lifecycle of the Pod, and different types of PVs can be created based on different StorageClass types.
PersistentVolumeClaim (PVC): A storage request within a cluster. For example, a PV is similar to a Pod that uses node resources, while a PVC declares that a PV resource is used. A PVC can also dynamically create PVs when PV resources are insufficient.

### Considerations

- CBS cloud disks cannot be mounted across availability zones. If a Pod with a CBS-type PV mounted is migrated to another availability zone, the mount will fail.
- The TKE console does not support capacity expansion/reduction for CBS cloud disks. If needed, please do so in the CBS console.

## Operation Guide for PVs and PVCs in the Console

### Creating a PV Statically

Static creation of PVs is well suited for scenarios where an existing cloud disk is reused in a cluster.

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **Clusters** to go to the cluster management page.
3. Click the ID of the cluster where PV needs to be created to enter the cluster management page.
4. Select "Storage" > "PersistentVolume" to go to the PersistentVolume information page. See the figure below:
![PersistentVolume](https://main.qcloudimg.com/raw/ff7ad6cf8550150d425c04f466bfd78a.png)
5. Click **Create** to go to the "Create a PersistentVolume" page. See the figure below:
![Create a PersistentVolume](https://main.qcloudimg.com/raw/8bbef8e1e78d81667d274938cb94eed5.png)
6. Set the PV parameters based on actual needs. Key parameters are as follows:
 - Source setting: Set based on actual needs. The default option is "Static creation".
 - Name: Custom.
 - Select a cloud disk: Select based on actual needs.
 - StorageClass: Select based on actual needs.
7. Click **Create a PersistentVolume** to complete the creation.

<span id="createPVC2"></span>
### Creating a PVC

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **Clusters** to go to the cluster management page.
3. Click the ID of the cluster where PVC needs to be created to enter the cluster management page.
4. Select "Storage" > "PersistentVolumeClaim" to go to the PersistentVolumeClaim information page. See the figure below:
![PersistentVolumeClaim](https://main.qcloudimg.com/raw/cad8818416ee085d08c515f5314efafe.png)
5. Click **Create** to go to the "Create a PersistentVolumeClaim" page. See the figure below:
![Create a PersistentVolume](https://main.qcloudimg.com/raw/c24dd1c6b2d8b32cc766e8d8c1f11aa1.png)
6. Set the PVC parameters based on actual needs. Key parameters are as follows:
 - Name: Custom.
 - Namespace: Select the namespace type based on actual needs.
 - StorageClass: Select based on actual needs.
 - Capacity: Set based on actual needs.
7. Click **Create a PersistentVolumeClaim** to complete the creation.
 If the existing PVs are insufficient, the system will automatically create a PV.

### Creating a Workload to Use a PVC Volume

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **Clusters** to go to the cluster management page.
3. Click the ID of the cluster where workload needs to be deployed to enter the cluster management page.
4. Under "Workload", select a workload type to go to the corresponding information page. For example, select "Workload" > "DaemonSet" to go to the DaemonSet information page. See the figure below:
![](https://main.qcloudimg.com/raw/6d806f92378fcfe6a69c8a0df0222051.png)
5. Click **Create** to go to the "Create a workload" page.
6. Set the workload name, namespace and other information as instructed. In "Volume", click **Add a volume** to add a volume. See the figure below:
![Add a volume](https://main.qcloudimg.com/raw/f1a0c283d6876b9c642bbb52f6f0963e.png)
7. Select "Use an existing PVC" and enter the name to use an existing PVC. See the figure below:
![Use an existing PVC](https://main.qcloudimg.com/raw/027c61ba3f41499ec2141e33e3a37f7e.png)
9. Click **Create a workload** to complete the creation.

## Using kubectl to Manipulate PVs and PVCs

Currently, this is only supported for CBS-type PVs and PVCs. You can specify the type of cloud disk bound to a PV in [StorageClass Management](https://intl.cloud.tencent.com/document/product/457/30680). The following is a sample where which you can perform creation directly using kubectl.

<span id="createPV"></span>
### (Optional) Creating a PV

Create a PV using an existing CBS cloud disk. If no PV has been created, the system will create a corresponding PV automatically when [creating a PVC](#Creating a PVC).
```Yaml
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
      cbsDiskId: disk-xxxxxxx ## Specify an existing CBS id
      fsType: ext4
  storageClassName: cbs
```

<span id="createPVC"></span>
### Creating a PVC

If [no PV has been created](#Creating a PVC), the system will create a corresponding PV automatically when creating a PVC. Below is a YAML sample:
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
- The capacity of an HDD cloud disk must be a multiple of 10, with a minimum of 10.
- The minimum capacity of a premium cloud disk is 50 GB.
- The minimum capacity of an SSD cloud disk is 200 GB. For details, see the [CBS documentation](https://intl.cloud.tencent.com/document/product/362).

### Using a PVC

Below is a YAML sample:
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
