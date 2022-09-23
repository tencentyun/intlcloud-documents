## Overview

TKE supports online expansion of PVs, as well as the corresponding CBS and file system. Expansion can be completed without the need to restart pods. To ensure the stability of the file system, we recommend that you perform this operation when the CBS file system is not mounted.


## Prerequisites

- You have created a TKE cluster of v1.16 or later versions. For more information, see [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/30637).
- You have updated [CBS-CSI](https://github.com/TencentCloud/kubernetes-csi-tencentcloud/blob/master/docs/README_CBS.md) to the latest version.
- (Optional) You can use snapshot to back up data before expansion to avoid data loss due to expansion failure.


## Directions

### Creating a StorageClass that allows expansion

You can use the following YAML to create a StorageClass that allows expansion. Set `allowVolumeExpansion` to `true` in the Storageclass. Below is an example:

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


### Online expansion

Two expansion methods are provided:

| Expansion Method | Description |
| --------------------------- | ------------------------------------------------------------ |
|Online expansion with restarting the Pod | The CBS document system to be expanded is not mounted, and expansion errors and issues in method 2 can be avoided. **We recommend that you use this method for expansion**. |
|Online expansion without restarting the Pod | The CBS document system to be expanded is mounted on the node. If there is an I/O process, a document system expansion error may occur.|



<dx-tabs>
::: Online expansion with restarting the Pod

1. Run the following command to confirm the status of the PV and the document system before expansion. In the following example, the size of both PV and document system is 30G.
   <dx-codeblock>
   ::: plaintext
   $ kubectl exec ivantestweb-0 df /usr/share/nginx/html
   Filesystem     1K-blocks  Used Available Use% Mounted on
   /dev/vdd        30832548 44992  30771172   1% /usr/share/nginx/html

$ kubectl get pv pvc-e193201e-6f6d-48cf-b96d-ccc09225cf9c 
NAME                                       CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM                        STORAGECLASS   REASON   AGE
pvc-e193201e-6f6d-48cf-b96d-ccc09225cf9c   30Gi       RWO            Delete           Bound    default/www1-ivantestweb-0   cbs-csi                 20h
:::
</dx-codeblock>

2. Run the following command to tag the PV object with an invalid zone label, which aims to make the Pod unable to be scheduled to a node after it is restarted in the next step. Below is an example:
   <dx-codeblock>
   ::: plaintext
   $ kubectl label pv pvc-e193201e-6f6d-48cf-b96d-ccc09225cf9c failure-domain.beta.kubernetes.io/zone=nozone
   :::
   </dx-codeblock>
3. Run the following command to restart the Pod. The Pod will be in the `Pending` status because the label of the PV corresponding to the Pod indicates that it is in an invalid zone. Below is an example:
   <dx-codeblock>
   ::: plaintext
   $ kubectl delete pod ivantestweb-0

$ kubectl get pod ivantestweb-0
NAME            READY   STATUS    RESTARTS   AGE
ivantestweb-0   0/1     Pending   0          25s

$ kubectl describe pod ivantestweb-0
Events:
  Type     Reason            Age                 From               Message

----     ------            ----                ----               -------

  Warning  FailedScheduling  40s (x3 over 2m3s)  default-scheduler  0/1 nodes are available: 1 node(s) had no available volume zone.
:::
</dx-codeblock>

4. Run the following command to expand the capacity of the PVC object to 40G. Below is an example:
   <dx-codeblock>
   ::: plaintext
   kubectl patch pvc www1-ivantestweb-0 -p '{"spec":{"resources":{"requests":{"storage":"40Gi"}}}}'
   :::
   </dx-codeblock>

>! The PVC object capacity after expansion must be a multiple of 10. For more information on the storage capacity specifications supported by different cloud disk types, see [Creating Cloud Disks](https://intl.cloud.tencent.com/document/product/362/5744).

5. Run the following command to remove the label of the PVC object. In this way, the Pod can be scheduled successfully. Below is an example:
   <dx-codeblock>
   ::: plaintext
   $ kubectl label pv pvc-e193201e-6f6d-48cf-b96d-ccc09225cf9c failure-domain.beta.kubernetes.io/zone-
   persistentvolume/pvc-e193201e-6f6d-48cf-b96d-ccc09225cf9c labeled
   :::
   </dx-codeblock>
6. Run the following command. You can see that the status of the Pod is `Running`, and the size of both the corresponding PV and document system has expanded from 30G to 40G. Below is an example:
   <dx-codeblock>
   ::: plaintext
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
:::
</dx-codeblock>
:::
::: Online expansion without restarting the Pod

1. Run the following command to confirm the status of the PV and the document system before expansion. In the following example, the size of both PV and document system is 20G.
   <dx-codeblock>
   ::: plaintext
   $ kubectl exec ivantestweb-0 df /usr/share/nginx/html
   Filesystem     1K-blocks  Used Available Use% Mounted on
   /dev/vdd        20511312 45036  20449892   1% /usr/share/nginx/html

$ kubectl get pv pvc-e193201e-6f6d-48cf-b96d-ccc09225cf9c
NAME                                       CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM                        STORAGECLASS   REASON   AGE
pvc-e193201e-6f6d-48cf-b96d-ccc09225cf9c   20Gi       RWO            Delete           Bound    default/www1-ivantestweb-0   cbs-csi                 20h
:::
</dx-codeblock>

2. Run the following command to expand the capacity of the PVC object to 30G. Below is an example:
   <dx-codeblock>
   ::: plaintext
   $ kubectl patch pvc www1-ivantestweb-0 -p '{"spec":{"resources":{"requests":{"storage":"30Gi"}}}}'
   :::
   </dx-codeblock>

>! The PVC object capacity after expansion must be a multiple of 10. For more information on the storage capacity specifications supported by different cloud disk types, see [Creating Cloud Disks](https://intl.cloud.tencent.com/document/product/362/5744).

3. Run the following command. You can see that the size of both PV and document system has expanded to 30G. Below is an example:
   <dx-codeblock>
   ::: plaintext
   $ kubectl exec ivantestweb-0 df /usr/share/nginx/html
   Filesystem     1K-blocks  Used Available Use% Mounted on
   /dev/vdd        30832548 44992  30771172   1% /usr/share/nginx/html
   $ kubectl get pv pvc-e193201e-6f6d-48cf-b96d-ccc09225cf9c
   NAME                                       CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM                        STORAGECLASS   REASON   AGE
   pvc-e193201e-6f6d-48cf-b96d-ccc09225cf9c   30Gi       RWO            Delete           Bound    default/www1-ivantestweb-0   cbs-csi                 20h
   :::
   </dx-codeblock>
   :::
   </dx-codeblock>
   </dx-tabs>





