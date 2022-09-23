## Prerequisites


- You have created a TKE cluster of v1.18 or a later version. For more information, see [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/30637).
- You have installed the latest version of the [CBS-CSI](https://github.com/TencentCloud/kubernetes-csi-tencentcloud/blob/master/docs/README_CBS.md) add-on.


## Directions

### Using a snapshot to back up a cloud disk

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

### Restoring volumes from a snapshot (CBS)

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
