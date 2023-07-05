## Operation Scenario

CBS cloud disks do not support mounting to nodes across AZs. Therefore, in cross-AZ clusters, we recommend that you use the CBS-CSI **topology awareness** feature to avoid cross-AZ mounting problems.

## How it works

Topology-aware scheduling requires the cooperation of multiple Kubernetes components, including the Scheduler, PV controller, and external-provisioner. The detailed process is as follows:

1. The PV controller observes PVC objects and checks whether VolumeBindingMode of the Storageclass is **WaitForFirstConsumer**. If yes, it does not process the PVC creation event but waits for the Scheduler to process the event.
2. After the Scheduler schedules the pod, it will mark the nodeName on the PVC object as an annotation: `volume.kubernetes.io/selected-node: 10.0.0.72`.
3. After the PV controller obtains the update event of the PVC object, it processes the annotation (`volume.kubernetes.io/selected-node`), obtains the node object based on the nodeName, and then passes the node object to the external-provisioner.
4. The external-provisioner obtains the AZ based on the label of the passed node object (`failure-domain.beta.kubernetes.io/zone`) and then creates the PV in the corresponding AZ. In this way, the PV can be in the same AZ as the pod and you can avoid cross-AZ mounting problems.





## Prerequisites

- You have installed a TKE cluster of v1.14 or a later version. For more information, see [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/30637).
- You have updated [CBS-CSI](https://github.com/TencentCloud/kubernetes-csi-tencentcloud/blob/master/docs/README_CBS.md) or In-Tree to the latest version.


## Directions

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

