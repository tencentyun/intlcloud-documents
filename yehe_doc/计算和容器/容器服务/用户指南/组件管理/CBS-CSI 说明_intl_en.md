## Operation Scenario

The CBS-CSI add-on allows you to select the storage class and create the corresponding PVs and PVCs of the CBS type in a TKE cluster on the console. This document introduces the features of the CBS-CSI add-on and some common use cases.


## Features


| Feature | Description |
|---------|---------|
| Static volume | Supports manual creation of volumes, PV objects, and PVC objects. |
| Dynamic volume | Supports configuration, creation, and deletion of volumes and PV objects through StorageClass. |
| Storage topology awareness | CBS does not support cross-AZ mounting. In a cluster with multiple AZs, the CBS-CSI add-on will schedule pods first, and then volumes will be created in the AZ of the node where the pods are scheduled. |
| Scheduler awareness of node maxAttachLimit | By default, one Tencent CVM instance can mount up to 20 cloud disks. When scheduling pods, the scheduler will filter out nodes where the number of mounted cloud disks has exceeded the limit. |
| Online volume expansion | You can modify the PVC capacity field to implement online expansion (only the CBS type is supported). |
| Volume snapshot and restoration | Supports the creation of volumes through snapshots. |


## Component Description


After it is deployed in a cluster, the CBS-CSI add-on contains the following components:

- DaemonSet (NodePlugin): each node provides a DaemonSet. It consists of two containers, CBS-CSI Driver and node-driver-registrar. It is used to register the driver for the node and provide the ability to mount.
- StatefulSet and Deployment (Controller): consists of a driver and multiple sidecars (external-provisioner, external-attacher, external-resizer, external-snapshotter, and snapshot-controller). It provides functions, such as o create or delete volumes, attach or detach, expand, and take snapshot.

![](https://main.qcloudimg.com/raw/f469674c69e02fc912b65d0babc001bd.png)



## Limits

- TKE cluster version 1.14 or later
- You can expand cloud disks online and create snapshots in a TKE cluster only after using the CBS-CSI add-on.
- You can continue to use QcloudCbs (In-Tree plugin) in your TKE cluster. (It will be integrated to CBS-CSI through Volume Migration in the future.)



## Use Cases

### Case 1: use CBS-CSI to avoid cross-AZ mounting of cloud disks


CBS cloud disks do not support mounting to nodes across AZs. Therefore, in cross-AZ clusters, we recommend that you use the CBS-CSI **topology awareness** feature to avoid cross-AZ mounting problems.


#### How it works

Topology-aware scheduling requires the cooperation of multiple Kubernetes components, including the Scheduler, PV controller, and external-provisioner. The detailed process is as follows:

1. The PV controller observes PVC objects and checks whether VolumeBindingMode of the Storageclass is **WaitForFirstConsumer**. If yes, it does not process the PVC creation event but waits for the Scheduler to process the event.
2. After the Scheduler schedules the pod, it will mark the nodeName on the PVC object as an annotation: `volume.kubernetes.io/selected-node: 10.0.0.72`.
3. After the PV controller obtains the update event of the PVC object, it processes the annotation (`volume.kubernetes.io/selected-node`), obtains the node object based on the nodeName, and then passes the node object to the external-provisioner.
4. The external-provisioner obtains the AZ based on the label of the passed node object (`failure-domain.beta.kubernetes.io/zone`) and then creates the PV in the corresponding AZ. In this way, the PV can be in the same AZ as the pod and you can avoid cross-AZ mounting problems.





#### Prerequisites

- You have installed a TKE cluster of v1.14 or a later version. For more information, see [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/30637).
- You have updated [CBS-CSI](https://github.com/TencentCloud/kubernetes-csi-tencentcloud/blob/master/docs/README_CBS.md) or In-Tree to the latest version.


#### Directions

Use the following YAML to set volumeBindingMode to **WaitForFirstConsumer** in the Storageclass. See the sample code below:

```yaml
kind: StorageClass
metadata:
    name: cbs-topo
parameters:
    type: cbs
provisioner: com.tencent.cloud.csi.cbs
reclaimPolicy: Delete
volumeBindingMode: WaitForFirstConsumer
```

>? Both CBS-CSI and In-Tree support this operation.


### Case 2: expand cloud disks online

TKE supports online expansion of PVs as well as the corresponding CBS and file system. Expansion can be completed without the need to restart pods. To ensure the stability of the file system, we recommend that you perform this operation when the CBS file system is not mounted.


#### Prerequisites

- You have created a TKE cluster of v1.16 or a later version. For more information, see [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/30637).
- You have updated [CBS-CSI](https://github.com/TencentCloud/kubernetes-csi-tencentcloud/blob/master/docs/README_CBS.md) to the latest version.
- You can [use snapshots to back up data](#Case-3:-create-snapshots-and-use-them-to-restore-volumes) before expansion to avoid data loss if expansion fails. (optional)



#### Directions

#### Creating a StorageClass that supports expansion

Use the following YAML to create a StorageClass that allows expansion. In the StorageClass, set `allowVolumeExpansion` to `true`. See the sample code below:
```yaml
allowVolumeExpansion: true
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
   name: cbs-csi-expand
parameters:
   diskType: CLOUD_PREMIUM
provisioner: com.tencent.cloud.csi.cbs
reclaimPolicy: Delete
volumeBindingMode: Immediate
```


#### Online expansion

Two expansion methods are provided:

| Expansion Method | Description |
|---------|---------|
| Online expansion with pod restart | The CBS file system to be expanded is not mounted. This method can prevent expansion errors and the problems with method 2. **We recommend that you use this method to perform expansion.** |
| Online expansion without pod restart | The CBS file system to be expanded is mounted to the node. If the I/O process exists, file system expansion errors may occur. |




#### Online expansion with pods restart
1. Run the following command to confirm the status of the PV and file system before expansion. Below is a sample, in which the size of the PV and that of the file system are both 30 GB:

```
$ kubectl exec ivantestweb-0 df /usr/share/nginx/html
Filesystem     1K-blocks  Used Available Use% Mounted on
/dev/vdd        30832548 44992  30771172   1% /usr/share/nginx/html
$ kubectl get pv pvc-e193201e-6f6d-48cf-b96d-ccc09225cf9c 
NAME                                       CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM                        STORAGECLASS   REASON   AGE
pvc-e193201e-6f6d-48cf-b96d-ccc09225cf9c   30Gi       RWO            Delete           Bound    default/www1-ivantestweb-0   cbs-csi                 20h
```

2. Run the following command to attach an invalid-zone label to the PV object. This way, after the pod is restarted in the next step, it cannot be scheduled to a certain node. See the sample code below:

```
$ kubectl label pv pvc-e193201e-6f6d-48cf-b96d-ccc09225cf9c failure-domain.beta.kubernetes.io/zone=nozone
```

3. Run the following command to restart the pod. After the restart, because the label of the PV corresponding to the pod indicates an invalid zone, the pod will be in the Pending state. See the sample code below:

```
$ kubectl delete pod ivantestweb-0
$ kubectl get pod ivantestweb-0
NAME            READY   STATUS    RESTARTS   AGE
ivantestweb-0   0/1     Pending   0          25s
$ kubectl describe pod ivantestweb-0
Events:
  Type     Reason            Age                 From               Message
 ----     ------            ----                ----               -------
  Warning  FailedScheduling  40s (x3 over 2m3s)  default-scheduler  0/1 nodes are available: 1 node(s) had no available volume zone.

```
4. Run the following command to change the capacity in the PVC object to 40 GB. See the sample below:

```
kubectl patch pvc www1-ivantestweb-0 -p '{"spec":{"resources":{"requests":{"storage":"40Gi"}}}}'
```

5. Run the following command to remove the label attached to the PV object. After the label is removed, the pod can be scheduled successfully. See the sample below:

```
$ kubectl label pv pvc-e193201e-6f6d-48cf-b96d-ccc09225cf9c failure-domain.beta.kubernetes.io/zone-
persistentvolume/pvc-e193201e-6f6d-48cf-b96d-ccc09225cf9c labeled
```

6. Run the following command to confirm that the status of the pod is Running and that the corresponding PV and file system have been expanded from 30 GB to 40 GB. See the sample below:

```
$ kubectl get pod ivantestweb-0
NAME            READY   STATUS    RESTARTS   AGE
ivantestweb-0   1/1     Running   0          17m
$ kubectl get pv pvc-e193201e-6f6d-48cf-b96d-ccc09225cf9c
NAME                                       CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM                        STORAGECLASS   REASON   AGE
pvc-e193201e-6f6d-48cf-b96d-ccc09225cf9c   40Gi       RWO            Delete           Bound    default/www1-ivantestweb-0   cbs-csi                 20h
$ kubectl get pvc www1-ivantestweb-0
NAME                 STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS   AGE
www1-ivantestweb-0   Bound    pvc-e193201e-6f6d-48cf-b96d-ccc09225cf9c   40Gi       RWO            cbs-csi        20h
$ kubectl exec ivantestweb-0 df /usr/share/nginx/html
Filesystem     1K-blocks  Used Available Use% Mounted on
/dev/vdd        41153760 49032  41088344   1% /usr/share/nginx/html
```


#### Online expansion without restarting pods
1. Run the following command to confirm the status of the PV and file system before expansion. Below is a sample, in which the size of the PV and that of the file system are both 20 GB:

```
$ kubectl exec ivantestweb-0 df /usr/share/nginx/html
Filesystem     1K-blocks  Used Available Use% Mounted on
/dev/vdd        20511312 45036  20449892   1% /usr/share/nginx/html
$ kubectl get pv pvc-e193201e-6f6d-48cf-b96d-ccc09225cf9c
NAME                                       CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM                        STORAGECLASS   REASON   AGE
pvc-e193201e-6f6d-48cf-b96d-ccc09225cf9c   20Gi       RWO            Delete           Bound    default/www1-ivantestweb-0   cbs-csi                 20h
```

2. Run the following command to change the capacity in the PVC object to 30 GB. See the sample code below:

```
$ kubectl patch pvc www1-ivantestweb-0 -p '{"spec":{"resources":{"requests":{"storage":"30Gi"}}}}'
```

3. Run the following command to confirm that the capacity of the PV and file system has been expanded to 30 GB. See the sample code below:

```
$ kubectl exec ivantestweb-0 df /usr/share/nginx/html
Filesystem     1K-blocks  Used Available Use% Mounted on
/dev/vdd        30832548 44992  30771172   1% /usr/share/nginx/html
$ kubectl get pv pvc-e193201e-6f6d-48cf-b96d-ccc09225cf9c
NAME                                       CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM                        STORAGECLASS   REASON   AGE
pvc-e193201e-6f6d-48cf-b96d-ccc09225cf9c   30Gi       RWO            Delete           Bound    default/www1-ivantestweb-0   cbs-csi                 20h
```



<span id = "case3"></span>
### Case 3: create snapshots and use them to restore volumes


#### Prerequisites


- You have created a TKE cluster of v1.18 or a later version. For more information, see [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/30637).
- You have installed the latest version of the [CBS-CSI](https://github.com/TencentCloud/kubernetes-csi-tencentcloud/blob/master/docs/README_CBS.md) add-on.


#### Directions

#### Using a snapshot to back up a cloud disk

1. Use the following YAML to create a VolumeSnapshotClass object. See the sample code below:

```
apiVersion: snapshot.storage.k8s.io/v1beta1
kind: VolumeSnapshotClass
metadata: 
    name: cbs-snapclass
driver: com.tencent.cloud.csi.cbs
deletionPolicy: Delete
```

2. After creation, run the following command to view the VolumeSnapshotClass object information. See the sample code below:

```plaintext
$ kubectl get volumesnapshotclass
NAME            DRIVER                      DELETIONPOLICY   AGE
cbs-snapclass   com.tencent.cloud.csi.cbs   Delete           17m
```

<span id = "step"></span>
3. This document uses the snapshot name `new-snapshot-demo` as an example in the following YAML to create a VolumeSnapshot. See the sample code below:

```
apiVersion: snapshot.storage.k8s.io/v1beta1
kind: VolumeSnapshot
metadata: 
    name: new-snapshot-demo
spec: 
    volumeSnapshotClassName: cbs-snapclass
    source: 
    persistentVolumeClaimName: csi-pvc
```

4. Run the following command to confirm that the Volumesnapshot and Volumesnapshotcontent objects have been created successfully. If `READYTOUSE` is true, creation was successful. See the sample code below:

```plaintext
$ kubectl get volumesnapshot
NAME                READYTOUSE   SOURCEPVC            SOURCESNAPSHOTCONTENT   RESTORESIZE   SNAPSHOTCLASS   SNAPSHOTCONTENT                                    CREATIONTIME   AGE
new-snapshot-demo   true         www1-ivantestweb-0                           10Gi          cbs-snapclass   snapcontent-ea11a797-d438-4410-ae21-41d9147fe610   22m            22m
$ kubectl get volumesnapshotcontent
NAME                                               READYTOUSE   RESTORESIZE   DELETIONPOLICY   DRIVER                      VOLUMESNAPSHOTCLASS   VOLUMESNAPSHOT      AGE
snapcontent-ea11a797-d438-4410-ae21-41d9147fe610   true         10737418240   Delete           com.tencent.cloud.csi.cbs   cbs-snapclass         new-snapshot-demo   22m
```

5. Run the following command to obtain the snapshot ID of the Volumesnapshotcontent object from the field `status.snapshotHandle` (snap-e406fc9m in the sample below). With the snapshot ID, you can go to the [TKE console](https://console.cloud.tencent.com/tke2) to check whether the snapshot exists. See the sample code below:

```
$ kubectl get volumesnapshotcontent snapcontent-ea11a797-d438-4410-ae21-41d9147fe610 -oyaml
apiVersion: snapshot.storage.k8s.io/v1beta1
kind: VolumeSnapshotContent
metadata:
    creationTimestamp: "2020-11-04T08:58:39Z"
    finalizers:
  - snapshot.storage.kubernetes.io/volumesnapshotcontent-bound-protection
    name: snapcontent-ea11a797-d438-4410-ae21-41d9147fe610
    resourceVersion: "471437790"
    selfLink: /apis/snapshot.storage.k8s.io/v1beta1/volumesnapshotcontents/snapcontent-ea11a797-d438-4410-ae21-41d9147fe610
    uid: 70d0390b-79b8-4276-aa79-a32e3bdef3d6
spec:
    deletionPolicy: Delete
    driver: com.tencent.cloud.csi.cbs
    source:
    volumeHandle: disk-7z32tin5
    volumeSnapshotClassName: cbs-snapclass
    volumeSnapshotRef:
    apiVersion: snapshot.storage.k8s.io/v1beta1
    kind: VolumeSnapshot
    name: new-snapshot-demo
    namespace: default
    resourceVersion: "471418661"
    uid: ea11a797-d438-4410-ae21-41d9147fe610
status:
    creationTime: 1604480319000000000
    readyToUse: true
    restoreSize: 10737418240
    snapshotHandle: snap-e406fc9m
```

#### Restoring volumes from a snapshot (CBS)

1. This document uses the VolumeSnapshot object, named `new-snapshot-demo` and created in the preceding [step](#step), as an example to show the process for restoring a volume from the snapshot. See the sample code below:

```
apiVersion: v1
kind: PersistentVolumeClaim
metadata: 
    name: restore-test
spec: 
    storageClassName: cbs-csi
    dataSource: 
    name: new-snapshot-demo
    kind: VolumeSnapshot
    apiGroup: snapshot.storage.k8s.io
    accessModes: 
    - ReadWriteOnce 
      resources: 
    requests: 
      storage: 10Gi
```

2. Run the following command to confirm that the restored PVC has been created successfully. From the PV, you can view the corresponding diskid (disk-gahz1kw1 in the sample below). See the sample code below:

```
$ kubectl get pvc restore-test
NAME           STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS   AGE
restore-test   Bound    pvc-80b98084-29a3-4a38-a96c-2f284042cf4f   10Gi       RWO            cbs-csi        97s
$ kubectl get pv pvc-80b98084-29a3-4a38-a96c-2f284042cf4f -oyaml
apiVersion: v1
kind: PersistentVolume
metadata:
  annotations:
    pv.kubernetes.io/provisioned-by: com.tencent.cloud.csi.cbs
  creationTimestamp: "2020-11-04T12:08:25Z"
  finalizers:
  - kubernetes.io/pv-protection
    name: pvc-80b98084-29a3-4a38-a96c-2f284042cf4f
    resourceVersion: "474676883"
    selfLink: /api/v1/persistentvolumes/pvc-80b98084-29a3-4a38-a96c-2f284042cf4f
    uid: 5321df93-5f21-4895-bafc-71538d50293a
spec:
    accessModes:
  - ReadWriteOnce
    capacity:
    storage: 10Gi
    claimRef:
    apiVersion: v1
    kind: PersistentVolumeClaim
    name: restore-test
    namespace: default
    resourceVersion: "474675088"
    uid: 80b98084-29a3-4a38-a96c-2f284042cf4f
    csi:
    driver: com.tencent.cloud.csi.cbs
    fsType: ext4
    volumeAttributes:
      diskType: CLOUD_PREMIUM
      storage.kubernetes.io/csiProvisionerIdentity: 1604478835151-8081-com.tencent.cloud.csi.cbs
    volumeHandle: disk-gahz1kw1
    nodeAffinity:
    required:
      nodeSelectorTerms:
      - matchExpressions:
        - key: topology.com.tencent.cloud.csi.cbs/zone
          operator: In
          values:
          - ap-beijing-2
      persistentVolumeReclaimPolicy: Delete
      storageClassName: cbs-csi
      volumeMode: Filesystem
status:
      phase: Bound
```
