## Operation Scenarios

If you need to create a snapshot of the PVC data disk to backup data, or to restore the backup snapshot data to a new PVC, you can use the CBS-CSI add-on. This document describes how to use the CBS-CSI add-on to implement data backup and restoration of PVC.


## Prerequisites

- You have created a [TKE cluster](https://intl.cloud.tencent.com/document/product/457/30637) or created a Kubernetes cluster in Tencent Cloud CVM. The cluster version is v1.18 or later.
- You have installed [CBS-CSI add-on](https://github.com/TencentCloud/kubernetes-csi-tencentcloud/blob/master/docs/README_CBS.md).
- You have granted related permissions of CBS snapshot for `TKE_QCSRole` on the [Access Management](https://console.cloud.tencent.com/cam/role) page of the console. For details, see [CBS-CSI](https://intl.cloud.tencent.com/document/product/457/39136).

## Operation Directions

### Restoring PVC

#### Creating a VolumeSnapshotClass

1. Use the following YAML to create a VolumeSnapshotClass object, as shown below:
```yaml
apiVersion: snapshot.storage.k8s.io/v1beta1
kind: VolumeSnapshotClass
metadata:
      name: cbs-snapclass
driver: com.tencent.cloud.csi.cbs
deletionPolicy: Delete
```
2. Run the following command to check whether the VolumeSnapshotClass has been created successfully, as shown below:
```bash
$ kubectl get volumesnapshotclass
NAME            DRIVER                      DELETIONPOLICY   AGE
cbs-snapclass   com.tencent.cloud.csi.cbs   Delete           17m
```

#### Create a PVC snapshot object VolumeSnapshot

1. [](id:volumesnapshot)This document takes `new-snapshot-demo` as the snapshot name to create a VolumeSnapshot. Use the following YAML to create a VolumeSnapshot object, as shown below:
```yaml
apiVersion: snapshot.storage.k8s.io/v1beta1
kind: VolumeSnapshot
metadata:
      name: new-snapshot-demo
spec:
      volumeSnapshotClassName: cbs-snapclass # Use the VolumeSnapshotClass created in the above steps
      source:
        persistentVolumeClaimName: ssd-pvc # Replace it with the PVC name that needs to be backed up
```
2. Run the following command to check whether the Volumesnapshot and Volumesnapshotcontent objects have been created successfully. If `READYTOUSE` is true, the creation is successful, as shown below:
```plaintext
$ kubectl get volumesnapshot
NAME                READYTOUSE   SOURCEPVC   SOURCESNAPSHOTCONTENT   RESTORESIZE   SNAPSHOTCLASS   SNAPSHOTCONTENT                                    CREATIONTIME   AGE
new-snapshot-demo   true         ssd-pvc                             20Gi          cbs-snapclass   snapcontent-170b2161-f158-4c9e-a090-a38fdfd84a3e   2m36s          2m50s
$ kubectl get volumesnapshotcontent
NAME                                               READYTOUSE   RESTORESIZE   DELETIONPOLICY   DRIVER                      VOLUMESNAPSHOTCLASS   VOLUMESNAPSHOT      AGE
snapcontent-170b2161-f158-4c9e-a090-a38fdfd84a3e   true         21474836480   Delete           com.tencent.cloud.csi.cbs   cbs-snapclass         new-snapshot-demo   3m3s
```
3. Run the following command to obtain the snapshot ID of the Volumesnapshotcontent object. The field is `status.snapshotHandle` (here takes snap-rsk8v75j as an example). You can log in to the [TKE console](https://console.cloud.tencent) .com/tke2) and use the snapshot ID to check whether the snapshot exists, as shown below:
```plaintext
$ kubectl get volumesnapshotcontent -o yaml snapcontent-170b2161-f158-4c9e-a090-a38fdfd84a3e
...
status:
  creationTime: 1607331318000000000
  readyToUse: true
  restoreSize: 21474836480
  snapshotHandle: snap-rsk8v75j
```

### Restoring data from the snapshot to a new PVC

1. This document takes the VolumeSnapshot object `new-snapshot-demo` created in the above [step](#volumesnapshot) as an example. Use the following YAML to restore data from the snapshot to a new PVC, as shown below:
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
      name: restore-test
spec:
      storageClassName: ssd-csi # Customize the storage class as needed
      dataSource:
        name: new-snapshot-demo # Use the VolumeSnapshot created in the above step
        kind: VolumeSnapshot
        apiGroup: snapshot.storage.k8s.io
      accessModes:
        - ReadWriteOnce # CBS is block storage, which only supports single machine read and write
      resources:
        requests:
          storage: 50Gi # The recommended storage capacity is the same as the capacity of the restored PVC
```
2. Run the following command. You can check that the PVC has been created and bound to the PV, and you can find the corresponding diskid (here takes disk-ju0hw7no as an example) in the PV, as shown below:
``` bash
$ kubectl get pvc restore-test
NAME           STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS   AGE
restore-test   Bound    pvc-940edf09-d622-4126-992b-0a209f048c7d   60Gi       RWO            ssd-topology   6m8s
$ kubectl get pv pvc-940edf09-d622-4126-992b-0a209f048c7d -o yaml
...
spec:
...
    volumeHandle: disk-ju0hw7no
...
```
>? If StorageClass uses topology awareness (schedule the Pod first and then create the PV), that is, to specify `volumeBindingMode: WaitForFirstConsumer`, you need to deploy the Pod (to mount the PVC) to trigger the creation of the PV (create a new CBS from the snapshot and bind it to the PV).
