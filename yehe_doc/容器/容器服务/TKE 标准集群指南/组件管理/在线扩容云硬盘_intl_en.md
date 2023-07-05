## Operation Scenario

TKE supports online expansion of PVs as well as the corresponding CBS and file system. Expansion can be completed without the need to restart pods. To ensure the stability of the file system, we recommend that you perform this operation when the CBS file system is not mounted.


## Prerequisites

- You have created a TKE cluster of v1.16 or a later version. For more information, see [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/30637).
- You have updated [CBS-CSI](https://github.com/TencentCloud/kubernetes-csi-tencentcloud/blob/master/docs/README_CBS.md) to the latest version.
- You can [use snapshots to back up data](#Case-3:-create-snapshots-and-use-them-to-restore-volumes) before expansion to avoid data loss if expansion fails. (optional)



## Directions

### Creating a StorageClass that supports expansion

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


### Online expansion

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
