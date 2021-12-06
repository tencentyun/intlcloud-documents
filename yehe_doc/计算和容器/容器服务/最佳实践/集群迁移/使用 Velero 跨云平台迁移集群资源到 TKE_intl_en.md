## Overview

The open source tool [Velero](https://velero.io/) (formerly known as the Heptio Ark) can safely back up and restore, perform disaster recovery, and migrate Kubernetes cluster resources and persistent volumes. TKE supports using Velero to back up, restore and migrate cluster resources. For more information, see [Using COS as Velero Storage to Implement Backup and Restoration of Cluster Resources](https://intl.cloud.tencent.com/zh/document/product/457/38939) and [Using Velero to Migrate and Replicate Cluster Resources in TKE](https://intl.cloud.tencent.com/zh/document/product/457/38940). This document describes how to use Velero to seamlessly migrate self-built or other cloud platform Kubernetes clusters to TKE.

## Migration Principle

The principle of using Velero to migrate self-built or other cloud platform cluster is similar to the principle of [Using Velero to Replicate Cluster Resources in TKE](https://intl.cloud.tencent.com/zh/document/product/457/38940). Both the source cluster and the target cluster for migration need to install Velero instances and specify the same Tencent Cloud [COS](https://intl.cloud.tencent.com/zh/document/product/436) bucket. According to the actual needs, the source cluster performs backup, and the target cluster restores cluster resources, so as to implement resource migration.
The difference is that when you migrate cluster resources from self-built or other cloud platforms to TKE, you need to consider and solve the problem of cluster environment differences caused by cross-platform. You can refer to the practical backup and restore strategies provided by Velero to solve the problems.



## Prerequisites

- There is a self-built or other cloud platform Kubernetes cluster (cluster A), and the cluster version must be v1.10 or later.
- There is a target TKE cluster (cluster B). For how to create a TKE cluster, see [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/30637).
- Both cluster A and cluster B need to install Velero instances (v1.5 or later version), and share the same COS bucket as Velero backend storage. For the installation steps, see [Configuring COS and Installing Velero](https://intl.cloud.tencent.com/zh/document/product/457/38939).
- Ensure that image resources can be pulled normally after migration.
- It is recommended that the two clusters use the same Kubernetes version to ensure the APIs are compatible.

## Migration Guide

Before migration, it is recommended that you make a detailed migration plan, and consider the following points during the migration process:


<dx-accordion>
::: Analyzing and filtering which cluster resources need to migrate
Filter and classify the resource inventories that need migration and that do not need migration based on actual needs.
:::
::: Considering whether you need to customize the Hook operation according to the business scenario
<li>When backing up cluster resources, you need to consider whether to perform <a href="https://velero.io/docs/v1.5/backup-hooks/">Backup Hooks</a> during the backup. For example, the memory data of the running application needs to be stored in disk.</li>
<li>When restoring (migrating) cluster resources, you need to consider whether to perform <a href="https://velero.io/docs/v1.5/backup-hooks/">Restoring Hooks</a> during the restoration. For example, some initialization work needs to be prepared before restoration.</li>
:::
::: Writing backup and restoration commands or resource inventories as needed
Write backup and restoration strategies based on the filtered and classified resource inventories. It is recommended to use the method of creating resource inventories to perform backup and restoration in complex scenarios. The YAML resource inventory is intuitive and easy to maintain. For simple migration or test scenarios, you can specify parameters to implement backup and restoration.
:::
::: Processing resource differences across cloud platforms
Due to the cross-cloud platform migration, the relationships of the dynamic storage classes for creating PVC may be different. You need to plan in advance whether the relationships of dynamic PVC/PV storage classes need to be remapped. And you need to create the ConfigMap configuration of the relevant mapping before the restoration. To solve more personalized differences, you can manually modify the backup resource inventory.
:::
::: Checking the migrated resources after migration
 Check whether the migrated cluster resources meet expectations and the data is complete and available.
:::
</dx-accordion>




## Directions

The following describes the detailed steps of migrating resources from a cloud platform cluster A to TKE cluster B. For the involved the basic knowledge of Velero backup and restoration, please refer to [Practical Velero backup/restoration Knowledge](#veleroknow).



### Creating the resources of cluster A

Deploy an Nginx workload with PVC in Velero instance in cluster A. For convenience, you can directly use dynamic storage class to create PVC and PV.
1. Run the following command to view the dynamic storage class information supported by the current cluster, as shown below:
```bash
# Get the storage class information supported by the current cluster, where xxx-StorageClass is the storage class code name, and xxx-Provider is the provider code name (the same below).
$ kubectl  get sc
NAME                PROVISIONER    RECLAIMPOLICY   VOLUMEBINDINGMODE      ALLOWVOLUMEEXPANSION   AGE
xxx-StorageClass    xxx-Provider   Delete          Immediate              true                   3d3h
...
```
2. Modify the PVC resource inventory in the [with-pv.yaml](https://github.com/vmware-tanzu/velero/blob/v1.5.1/examples/nginx-app/with-pv.yaml) file, and use the storage class named "xxx-StorageClass" in the cluster to dynamically create, as shown below:
<dx-codeblock>
:::  yaml
...
---
kind: PersistentVolumeClaim
apiVersion: v1
metadata: 
  name: nginx-logs
  namespace: nginx-example
  labels: 
    app: nginx
spec: 
  # Optional: modify the value of the PVC storage class to the cloud platform of cluster A. 
  storageClassName: xxx-StorageClass 
  accessModes: 
    - ReadWriteOnce
  resources: 
    requests: 
      storage: 20Gi # Since the minimum storage of this cloud platform is 20 Gi, you need to modify the storage to 20 Gi in this sample.
... 
:::
</dx-codeblock>
3. Run the following command to apply with-pv.yaml in the sample to create the following cluster resources (nginx-example namespace), as shown below:
```bash
$ kubectl apply -f with-pv.yaml 
namespace/nginx-example created
persistentvolumeclaim/nginx-logs created
deployment.apps/nginx-deployment created
service/my-nginx created
```
4. The created PVC “nginx-logs” has been mounted to the `/var/log/nginx` directory of the Nginx container as the log storage of service. The sample here will test and access the Nginx service in the browser to generate log data for the mounted PVC for data comparison after restoration, as shown below:
<dx-codeblock>
:::  bash
$ kubectl exec -it nginx-deployment-5ccc99bffb-6nm5w bash -n nginx-example
kubectl exec [POD] [COMMAND] is DEPRECATED and will be removed in a future version. Use kubectl kubectl exec [POD] -- [COMMAND]
Defaulting container name to nginx.
Use 'kubectl describe pod/nginx-deployment-5ccc99bffb-6nm5w -n nginx-example' to see all of the containers in this pod 

$ du -sh /var/log/nginx/
84K /var/log/nginx/

# View the first two logs of accss.log and error.log.
$ head -n 2 /var/log/nginx/access.log 
192.168.0.73 - - [29/Dec/2020:03:02:31 +0000] "GET /?spm=5176.2020520152.0.0.22d016ddHXZumX HTTP/1.1" 200 612 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/87.0.4280.88 Safari/537.36" "-"
192.168.0.73 - - [29/Dec/2020:03:02:32 +0000] "GET /favicon.ico HTTP/1.1" 404 555 "http://47.242.233.22/?spm=5176.2020520152.0.0.22d016ddHXZumX" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/87.0.4280.88 Safari/537.36" "-"

$ head -n 2 /var/log/nginx/error.log 
2020/12/29 03:02:32 [error] 6#6: *597 open() "/usr/share/nginx/html/favicon.ico" failed (2: No such file or directory), client: 192.168.0.73, server: localhost, request: "GET /favicon.ico HTTP/1.1", host: "47.242.233.22", referrer: "http://47.242.233.22/?spm=5176.2020520152.0.0.22d016ddHXZumX"
2020/12/29 03:07:21 [error] 6#6: *1172 open() "/usr/share/nginx/html/0bef" failed (2: No such file or directory), client: 192.168.0.73, server: localhost, request: "GET /0bef HTTP/1.0"
:::
</dx-codeblock>




### Confirming the resource inventories to migrate

1. Run the following command to output all resource inventories in cluster A.
```bash
kubectl api-resources --verbs=list -o name  | xargs -n 1 kubectl get --show-kind --ignore-not-found --all-namespaces
```
 You can also run the following commands to distinguish namespaces based on resources and narrow the scope of output resources:
	- View the resource inventories that do not distinguish namespaces:
		 ```bash
		 kubectl api-resources --namespaced=false --verbs=list -o name | xargs -n 1 kubectl get --show-kind --ignore-not-found
		 ```
	- View the resource inventories that distinguish namespaces:
		 ```bash
		 kubectl api-resources --namespaced=true --verbs=list -o name | xargs -n 1 kubectl get --show-kind --ignore-not-found --all-namespaces
		 ```
2. You can filter the resource inventories that need to migrate based on the actual needs. The sample here will directly migrate Nginx workload-related resources under the "nginx-example" namespace from this cloud platform to TKE. The resources involved are as follows:
<dx-codeblock>
:::  bash
$ kubectl  get all -n nginx-example
NAME                                    READY   STATUS    RESTARTS   AGE
pod/nginx-deployment-5ccc99bffb-tn2sh   2/2     Running   0          2d19h

NAME               TYPE           CLUSTER-IP     EXTERNAL-IP   PORT(S)        AGE
service/my-nginx   LoadBalancer   172.21.1.185   x.x.x.x   80:31455/TCP   2d19h

NAME                               READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/nginx-deployment   1/1     1            1           2d19h

NAME                                          DESIRED   CURRENT   READY   AGE
replicaset.apps/nginx-deployment-5ccc99bffb   1         1         1       2d19h

$ kubectl  get pvc -n nginx-example
NAME         STATUS   VOLUME                   CAPACITY   ACCESS MODES   STORAGECLASS              AGE
nginx-logs   Bound    d-j6ccrq4k1moziu1l6l5r   20Gi       RWO            xxx-StorageClass   2d19h

$ kubectl  get pv
NAME                     CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM                      STORAGECLASS              REASON   AGE
d-j6ccrq4k1moziu1l6l5r   20Gi       RWO            Delete           Bound    nginx-example/nginx-logs   xxx-StorageClass            2d19h
:::
</dx-codeblock>




### Confirming Hook strategy

The sample has configured a Hook strategy that is "setting the file system to read-only before backing up the Nginx workload and restoring it to read/write after the backup” in [with-pv.yaml](https://github.com/vmware-tanzu/velero/blob/v1.5.1/examples/nginx-app/with-pv.yaml). The YAML file is as follows:
<dx-codeblock>
:::  yaml
...
      annotations: 
        # The annotation of the backup hook strategy indicates that the nginx log directory is set to read-only mode before starting the backup, and is restored to read/write mode after the backup is completed.
        pre.hook.backup.velero.io/container: fsfreeze
        pre.hook.backup.velero.io/command: '["/sbin/fsfreeze", "--freeze", "/var/log/nginx"]'
        post.hook.backup.velero.io/container: fsfreeze
        post.hook.backup.velero.io/command: '["/sbin/fsfreeze", "--unfreeze", "/var/log/nginx"]'
    spec: 
      volumes: 
        - name: nginx-logs 
          persistentVolumeClaim: 
           claimName: nginx-logs 
      containers: 
      - image: nginx:1.17.6 
        name: nginx 
        ports: 
        - containerPort: 80 
        volumeMounts: 
          - mountPath: "/var/log/nginx"
            name: nginx-logs
            readOnly: false 
      - image: ubuntu:bionic
        name: fsfreeze
        securityContext: 
          privileged: true 
        volumeMounts: 
          - mountPath: "/var/log/nginx"
            name: nginx-logs
 ...
:::
</dx-codeblock>




### Starting migration

Write a backup and restoration strategy based on the actual situation, and begin to migrate the Nginx workload related resources of the cloud platform.




#### Performing backup in cluster A

1. Create the following YAML file to back up the resources that need to migrate.
    <dx-codeblock>
    :::  yaml
    apiVersion: velero.io/v1
    kind: Backup
    metadata: 
    name: migrate-backup
  # Must be the namespace installed by velero.
  namespace: velero
spec: 
  # The resources that only contains the nginx-example namespace.
  includedNamespaces: 
   - nginx-example
  # The resources that do not distinguish namespace.
  includeClusterResources: true 
  # Specify the storage location of the backup data.
  storageLocation: default 
  # Specify the storage location of the volume snapshot.
  volumeSnapshotLocations: 
    - default 
  # Use restic to back up the volume.
  defaultVolumesToRestic: true
:::
</dx-codeblock>
2. The backup process is shown below. When the backup status is "Completed" and the number of errors is 0, the backup process is complete and correct.
```bash
$ kubectl apply -f backup.yaml 
backup.velero.io/migrate-backup created
$ velero backup get 
NAME             STATUS      ERRORS   WARNINGS   CREATED                EXPIRES   STORAGE LOCATION   SELECTOR
migrate-backup   InProgress  0        0          2020-12-29 19:24:12 +0800 CST   29d    default     <none>
$ velero backup get 
NAME             STATUS      ERRORS   WARNINGS   CREATED                EXPIRES   STORAGE LOCATION   SELECTOR
migrate-backup   Completed   0        0          2020-12-29 19:24:28 +0800 CST   29d    default     <none>
```
3. After the backup is complete, run the following command to temporarily update the backup storage location to read-only mode, as shown below:
<dx-alert infotype="explain" title="">
This can prevent Velero from creating or deleting backup objects in the backup storage location during the restoration. (Optional)
</dx-alert>
```bash
kubectl patch backupstoragelocation default --namespace velero \
    --type merge \
    --patch '{"spec":{"accessMode":"ReadOnly"}}'
```



#### Processing resource differences across cloud platforms

1. Due to differences in the dynamic storage classes used, you need to create a dynamic storage class name mapping for the persistent volume "nginx-logs" through the ConfigMap shown below.
<dx-codeblock>
:::  yaml
apiVersion: v1
kind: ConfigMap
metadata: 
    name: change-storage-class-config
    namespace: velero
    labels: 
    velero.io/plugin-config: ""
    velero.io/change-storage-class: RestoreItemAction
data: 
  # Storage class name is mapped to Tencent cloud dynamic storage class cbs.
  xxx-StorageClass: cbs
:::
</dx-codeblock>
2. Run the following command to apply the above ConfigMap configuration, as shown below:
```bash
$ kubectl  apply -f cm-storage-class.yaml 
configmap/change-storage-class-config created
```
3. The resource inventories backed up by Velero is stored in COS in JSON format. If you have a more personalized migration requirement, you can directly download the backup file and customize it. The sample below will add a "jokey-test:jokey-test" annotation to the Deployment resource of Nginx. The modification process is as follows:
```bash
$ Downloads % mkdir migrate-backup
# Decompress the backup file.
$ Downloads % tar -zxvf migrate-backup.tar.gz  -C migrate-backup
# Edit the resources that need to be customized. In the sample below, "jokey-test" is added to the Deployment resource of Nginx: "jokey-test" annotation.
$ migrate-backup % cat  resources/deployments.apps/namespaces/nginx-example/nginx-deployment.json 
{"apiVersion":"apps/v1","kind":"Deployment","metadata":{"annotations":{"jokey-test":"jokey-test",...
# Repack the modified backup files.
$ migrate-backup % tar -zcvf migrate-backup.tar.gz *
```
4. Complete the custom modification and repackage, and log in to [COS console](https://console.cloud.tencent.com/cos5/bucket) to upload the backup file and replace the original backup file.
![](https://qcloudimg.tencent-cloud.cn/raw/f517bdca8aef76fa7cc5d69e519c5cf6.png)


#### Performing the restoration in cluster B

1. The sample uses the resource inventories shown below to perform the restoration (migration).
   <dx-codeblock>
   :::  yaml
   apiVersion: velero.io/v1
   kind: Restore
   metadata: 
    name: migrate-restore
    namespace: velero
   spec: 
    backupName: migrate-backup
    includedNamespaces: 
    - nginx-example

  # Fill in the resource type to be restored as needed. There is no resource to be excluded under the nginx-example namespace, so enter '*' here.
  includedResources: 
    - '*'

  includeClusterResources: null

  # Resources not included in the restoration. Here storageClasses resource types are excluded.
  excludedResources: 
    - storageclasses.storage.k8s.io

  # Use the labelSelector selector to select the resource with a specific label. Since there is no need to use the label selector to filter in this sample, please make an annotation here.
  # labelSelector:
  #   matchLabels:
  #     app: nginx

  # Set the relationship mapping strategy of the namespace.
  namespaceMapping: 
    nginx-example: default
  restorePVs: true
:::
</dx-codeblock>
2. The execution of the restoration process is shown below. When the restoration status is "Completed" and the number of "errors" is 0, it means the restoration process is complete and correct.
```bash
$ kubectl  apply -f restore.yaml 
restore.velero.io/migrate-restore created
$ velero restore get
NAME              BACKUP           STATUS      STARTED                         COMPLETED                       ERRORS   WARNINGS   CREATED                         SELECTOR
migrate-restore   migrate-backup   Completed   2021-01-12 20:39:14 +0800 CST   2021-01-12 20:39:17 +0800 CST   0        0          2021-01-12 20:39:14 +0800 CST   <none>
```


### Checking the migrated resources

1. Run the following command to check whether the running status of the migrated resource is normal, as shown below:
```bash
# Since the "nginx-example" namespace is specified to map to the "default" namespace when restoration, the restored resource will run under the "default" namespace. 
$ kubectl  get all -n default 
NAME                                    READY   STATUS    RESTARTS   AGE
pod/nginx-deployment-5ccc99bffb-6nm5w   2/2     Running   0          49s

NAME                 TYPE           CLUSTER-IP       EXTERNAL-IP      PORT(S)         AGE
service/kube-user    LoadBalancer   172.16.253.216   10.0.0.28        443:30060/TCP   8d
service/kubernetes   ClusterIP      172.16.252.1     <none>           443/TCP         8d
service/my-nginx     LoadBalancer   172.16.254.16    x.x.x.x          80:30840/TCP    49s

NAME                               READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/nginx-deployment   1/1     1            1           49s

NAME                                          DESIRED   CURRENT   READY   AGE
replicaset.apps/nginx-deployment-5ccc99bffb   1         1         1       49s
```
 From the command execution result, you can find that the running status of the migrated resource is normal.
2. Check whether the set restoration strategy is successful.
 1. Run the following command to check whether the mapping of the dynamic storage class name is correct, as shown below:
 ```bash
 # You can find that the storage class of PVC/PV is already "cbs", indicating that the storage class mapping is successful.
$ kubectl  get pvc -n default 
 NAME         STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS   AGE
 nginx-logs   Bound    pvc-bcc17ccd-ec3e-4d27-bec6-b0c8f1c2fa9c   20Gi       RWO            cbs            55s
$ kubectl  get pv 
 NAME                                       CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM                STORAGECLASS   REASON   AGE
 pvc-bcc17ccd-ec3e-4d27-bec6-b0c8f1c2fa9c   20Gi       RWO            Delete           Bound    default/nginx-logs   cbs                     57s
 ```
		 If the storage class of PVC/PV is "cbs", the storage class mapping is successful. From the execution result of the above command, you can find that the storage class mapping is successful.
 2. Run the following command to check whether the custom-added "jokey-test" annotation for "deployment.apps/nginx-deployment" before restoration is successful, as shown below:
```bash
# Obtain the annotation "jokey-test" successfully, indicating that the custom modification of the resource is successful.
$ kubectl  get deployment.apps/nginx-deployment -o custom-columns=annotations:.metadata.annotations.jokey-test
annotations
jokey-test
```
     If the annotations can be obtained normally, the custom resource has been modified successfully. From the execution result of the above command, you can find that the namespace mapping configuration is successful.
3. Run the following command to check whether the PVC data mounted by the workload is successfully migrated.
<dx-codeblock>
:::  bash
# Check the data size in the mounted PVC data directory. The data size is 88K, which is more than the size before the migration. The reason is that Tencent Cloud CLB actively initiated a health check and generated some logs.   
$ kubectl  exec -it nginx-deployment-5ccc99bffb-6nm5w -n default -- bash
Defaulting container name to nginx.
Use 'kubectl describe pod/nginx-deployment-5ccc99bffb-6nm5w -n default' to see all of the containers in this pod.

$ du -sh /var/log/nginx 
88K     /var/log/nginx

# Check the first two log information, which is the same as the log before the migration, indicating that the PVC data is not lost.
$ head -n 2 /var/log/nginx/access.log 
192.168.0.73 - - [29/Dec/2020:03:02:31 +0000] "GET /?spm=5176.2020520152.0.0.22d016ddHXZumX HTTP/1.1" 200 612 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/87.0.4280.88 Safari/537.36" "-"
192.168.0.73 - - [29/Dec/2020:03:02:32 +0000] "GET /favicon.ico HTTP/1.1" 404 555 "http://47.242.233.22/?spm=5176.2020520152.0.0.22d016ddHXZumX" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/87.0.4280.88 Safari/537.36" "-"

$ head -n 2 /var/log/nginx/error.log 
2020/12/29 03:02:32 [error] 6#6: *597 open() "/usr/share/nginx/html/favicon.ico" failed (2: No such file or directory), client: 192.168.0.73, server: localhost, request: "GET /favicon.ico HTTP/1.1", host: "47.242.233.22", referrer: "http://47.242.233.22/?spm=5176.2020520152.0.0.22d016ddHXZumX"
2020/12/29 03:07:21 [error] 6#6: *1172 open() "/usr/share/nginx/html/0bef" failed (2: No such file or directory), client: 192.168.0.73, server: localhost, request: "GET /0bef HTTP/1.0"
:::
</dx-codeblock>
 From the result of the above command, you can find that the PVC data mounted by the workload is successfully migrated. So far, the Nginx (nginx-example namespace) workload-related resources and data in the cluster A have been successfully migrated to TKE cluster B (default namespace).



## Summary


This document mainly describes the ideas and methods of using Velero to migrate the resources of the self-built or other cloud platform clusters to TKE, and shows the sample that the cluster resources in cluster A are successfully migrated to cluster B seamlessly. If you encounter scenarios that are not covered in this document during the actual migration, please [submit a ticket](https://console.intl.cloud.tencent.com/workorder).



## Appendix: Practical Velero Backup/Restoration Knowledge[](id:veleroknow)

Velero provides many useful backup and restoration strategies, as shown below:


### Resource filtering

Velero includes all objects in a backup or restoration when no filtering options are used. You can specify parameters to filter resources as needed during **backup and restoration**. For details, please refer to [Resource Filtering]( https://velero.io/docs/v1.5/resource-filtering/).
 - **Includes:**
<table>
<thead>
<tr>
<th style="width: 45%;">Parameters</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td><code>--include-resources</code></td>
<td>Specify a list of resource objects to include.</td>
</tr>
<tr>
<td><code>--include-namespaces</code></td>
<td>Specify a list of namespaces to include.</td>
</tr>
<tr>
<td><code>--include-cluster-resources</code></td>
<td>Specify whether to include resources of the cluster.</td>
</tr>
<tr>
<td><code>--selector</code></td>
<td>Specify to include the resources that match the label selector.</td>
</tr>
</tbody></table>

-  **Excludes:**
<table>
<thead>
<tr>
<th style="width: 45%;">Parameters</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td><code>--exclude-namespaces</code></td>
<td>Specify a list of namespaces to be excluded.</td>
</tr>
<tr>
<td><code>--exclude-resources</code></td>
<td>Specify a list of resource objects to be excluded.</td>
</tr>
<tr>
<td><code>velero.io/exclude-from-backup=true</code></td>
<td>This configuration item will configure this label attribute for the resource object, and the resource object with this label will be excluded.</td>
</tr>
</tbody></table>




### Hook operation

- Execute Hook operation during **backup**, for example, you need to store the memory data in disk before backup. For details, see [Backup Hooks](https://velero.io/docs/v1.5/backup-hooks/).
- Execute Hook operation during **restoration**, for example, you need to determine whether component dependencies are available before restoration. For details, see [Restore Hooks](https://velero.io/docs/v1.5/restore-hooks/).
- For configuring the mapping relationship between PVC/PV volumes during **restoration**, please refer to the following documents. For more details, see [Restore Reference](https://velero.io/docs/v1.5/restore-reference/).
  - [Changing PV/PVC Storage Classes](https://velero.io/docs/v1.5/restore-reference/#changing-pvpvc-storage-classes)
  - [Changing PVC selected-node](https://velero.io/docs/v1.5/restore-reference/#changing-pvc-selected-node)


### Configuration of using Restic to back up volume
Starting from Velero v1.5, Velero uses Restic to back up all Pod volumes by default instead of annotating each Pod separately. **Velero v1.5 or later is recommended**

For the Velero version that is earlier than v1.5, when Velero uses Restic to back up volumes, Restic provides the following two ways to find the Pod volumes that need to be backed up:
  - The used Pod volume backup selects to contain an annotation (default):
    ```bash
    kubectl -n <YOUR_POD_NAMESPACE> annotate <pod/YOUR_POD_NAME> backup.velero.io/backup-volumes=<YOUR_VOLUME_NAME_1,YOUR_VOLUME_NAME_2,...>
    ```
  - The used Pod volume backup selects to not contain an annotation:
    ```bash
    kubectl -n <YOUR_POD_NAMESPACE> annotate <pod/YOUR_POD_NAME> backup.velero.io/backup-volumes-excludes=<YOUR_VOLUME_NAME_1,YOUR_VOLUME_NAME_2,...>
    ```
#### Related commands
- After the backup is complete, run the following command to view the backup volume information:
  ```bash
  kubectl -n velero get podvolumebackups -l velero.io/backup-name=<YOUR_BACKUP_NAME> -o yaml
  ```
- After the restoration is complete, run the following command to view the restore volume information:
  ```bash
  kubectl -n velero get podvolumerestores -l velero.io/restore-name=<YOUR_RESTORE_NAME> -o yaml
  ```

### Other operations

- In addition to using the Velero command to perform the backup, it can also be triggered by **creating a backup resource (recommended)**. For the configuration example, see [Backup Example](https://velero.io/docs/v1.5/api- types/backup/#definition). For detailed API field definitions, see [Backup API Definition](https://github.com/vmware-tanzu/velero/blob/main/pkg/apis/velero/v1/backup.go).
- In addition to using the Velero command to perform the restoration, it can also be triggered by **creating a restoration resource (recommended)**. For the configuration example, see [Restoration Example](https://velero.io/docs/v1.5/api-types/restore/#definition). For detailed API field definitions, see [Restore API Definition](https://github.com/vmware-tanzu/velero/blob/main/pkg/apis/velero/v1/restore.go).
- If there are other personalized resource configurations such as annotations and label, you can manually edit the backup JSON resource inventory file before restoration.
