## Overview

[Velero](https://velero.io/) (the previous version is called Heptio Ark), an open-source tool, can safely back up and restore, perform disaster recovery, and migrate Kubernetes cluster resources and persistent volumes. Deploying Velero in the TKE cluster or self-built Kubenetes cluster, it can achieve the following features:
- Back up cluster resources and restore in case of loss.
- Migrate cluster resources to other clusters.
- Replicate the production cluster resources to development and test clusters.

For more information about Velero, see [Velero](https://velero.io/) official document. This document describes how to use Velero to seamlessly migrate and replicate cluster resources among TKE clusters.



## Migration Principle

Install Velero instances on both the cluster to migrate and the target cluster. The Velero instances of the two clusters point to the same [COS](https://intl.cloud.tencent.com/document/product/436 ) location. The process is as follows:
1. Use Velero to perform backup operations on the cluster that needs to migrate. Generate backup data and store it in the COS.
2. Use Velero to perform data restoration on the target cluster to implement migration.

The migration principle is shown as follows:
![velero](https://main.qcloudimg.com/raw/85706a906efb84e0931c2b432681fd94.png)



## Prerequisites

- You have registered a [Tencent Cloud account](https://intl.cloud.tencent.com/register).
- You have activated the [COS](https://console.cloud.tencent.com/cos5) service.
- There are already two TKE clusters: cluster A that needs to migrate and cluster B that has created a migration target. For how to create a TKE cluster, see [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/30637).
- Both cluster A and cluster B need to install Velero instances (v1.5 or later version), and share the same COS bucket as Velero backend storage. For the installation steps, see [Configuring Storage and Installing Velero](https://intl.cloud.tencent.com/document/product/457/38939#.E9.85.8D.E7.BD.AE.E5.AD.98.E5.82.A8).



## Notes

- Starting from Velero v1.5, Velero can use Restic to back up all Pod volumes without annotating each Pod individually. By default, users are allowed to use Restic to back up all Pod volumes, except for the following volumes:
   - The volumes that mount the default `Service Account Secret`
   - The type volumes that mount `hostPath`
   - The volumes that mount Kubernetes `secrets` and `configmaps`
This example requires Velero v1.5 or later version and [Restic](https://velero.io/docs/v1.5/restic/) enabled to back up persistent volume data. Please ensure that parameters `--use-restic` and `--default-volumes-to-restic` are enabled during the Velero installation. For the installation steps, see [Configuring Storage and Installing Velero](https://intl.cloud.tencent.com/document/product/457/38939#.E9.85.8D.E7.BD.AE.E5.AD.98.E5.82.A8).
- During the migration, it is not allowed to perform any CRUD operations on the resources of the clusters on both sides, so as to avoid data differences during the migration and data inconsistence after the final migration. 
- Please try to make sure that the CPU, memory and other specifications of cluster A and Cluster B are the same or do not differ too much, so as to avoid the situation that the migrated Pods cannot be scheduled due to resource reasons, resulting in Pending.


## Directions

### Creating a backup in cluster A



#### Checking cluster A resources before backup


Before backing up cluster A, you can view the resources and services of cluster A for [Migration Result Verification](#.E8.BF.81.E7.A7.BB.E7.BB.93.E6.9E.9C.E6.A0.B8.E9.AA.8C) after cluster restoration.

1. This document will compare and verify the resources of the “default” and “default2” namespaces. Run the following commands to view the Pods and PVC resources in the two namespaces in cluster A, as shown in the figure below:
![](https://main.qcloudimg.com/raw/f5c455c011d88bbfeac344d1dc51fbfd.png)
>?You can specify some custom Hook operations during the backup. For example, the data in the memory of the running application needs to be persisted to disk before backup. For more information about Hook, see [Backup Hooks](https://velero.io/docs/v1.5/backup-hooks/).
2. The MinIO COS in cluster A uses persistent volumes, and some images has been uploaded, as shown in the figure below:
![](https://main.qcloudimg.com/raw/b1260153686533a1384e2686ffe03fd1.png)

#### Cluster backup

1. Run the following command to back up all resources except the Velero namespace (the default namespace installed by Velero) in the cluster. If you need to customize the scope of the backup cluster resource, you can use the command `velero create backup -h` to view the available resource filter parameters.
```bash
velero backup create <BACKUP-NAME> --exclude-namespaces <NAMESPACE>
```
	This document takes the creation of a “default-all” cluster backup as an example. The backup process is shown in the figure below. If the status of the backup task is "Completed", the backup is successful.
	![](https://main.qcloudimg.com/raw/b6294ee314254d5524a9799bdf77112a.png)
>?You can also set regular automatic backups for Velero. Run the command `velero schedule -h` to view the setting method.
2. Run the following command to check if there is any errors in the backup operation. If the command does not produce any output, it means that no error occurred during the backup, as shown below:
```bash
velero backup logs <BACKUP-NAME> | grep error
```
	>!Please make sure that no errors occur during the backup. If Velero makes any errors during the backup, please re-perform the backup after troubleshooting.
3. After the backup is completed, run the following command to temporarily update the backup storage location to read-only mode (optional, to prevent Velero from creating or deleting backup objects in the backup storage location during the restoration), as shown below:
```bash
kubectl patch backupstoragelocation default --namespace velero \
			--type merge \
			--patch '{"spec":{"accessMode":"ReadOnly"}}'
```

### Performing a restoration in cluster B

#### Viewing cluster B resources before restoration

Before performing a restoration in cluster B, you can view the resources and services of cluster B for [Migration Result Verification](#.E8.BF.81.E7.A7.BB.E7.BB.93.E6.9E.9C.E6.A0.B8.E9.AA.8C) after cluster restoration.


Before the restoration, there are no workload resources under the “default” and “default2” namespaces in cluster B. Run the following commands to view the Pods and PVC resources in the two namespaces in cluster B, as shown below:
![image-20201118163640448](https://main.qcloudimg.com/raw/69447424d741418a88a85b7579fd124c.png)


#### Cluster restoration

1. Run the following command to temporarily update Velero backup storage location in cluster B to read-only mode (optional, to prevent Velero from creating or deleting backup objects in the backup storage location during the restoration), as shown below:
```bash
kubectl patch backupstoragelocation default --namespace velero \
			--type merge \
			--patch '{"spec":{"accessMode":"ReadOnly"}}'
```
	>?You can specify a custom Hook operation to perform during the restoration or after the resource restoration. For example, you need to perform a custom database restoration operation before the database application container starts. For more information about Hook, see [Restore Hooks](https://velero.io/docs/v1.5/restore-hooks/).

2. Before the restoration, you need to ensure that the Velero resource in cluster B is synchronized with the backup file in COS. You can use `--backup-sync-period` to configure the synchronization interval, which is 1 minute by default. You can run the following command to check whether the backup of cluster A has been synchronized.
```bash
velero backup get <BACKUP-NAME>
```
3. After the backup is successfully obtained and checked, run the following command to restore all contents to cluster B.
```bash
velero restore create --from-backup <BACKUP-NAME>
```
	The restoration process is shown in the figure below:
	![image-20201118175718281](https://main.qcloudimg.com/raw/13b5c653d6f64f800ef242567571408c.png)
4. After the restoration is completed, check the restoration log, and run the following command to check whether there are any errors and skips during restoration, as shown below:
```bash
# Check whether there are restoration errors during migration
velero restore logs <BACKUP-NAME> | grep error 
# View the skipped restoration operations during migration
velero restore logs <BACKUP-NAME> | grep skip
```
	As shown in the figure below, you can find that no errors occurred, but some "skipped" steps occurred during restoration. Because when backing up cluster resources, all cluster resources that did not contain the Velero namespace were backed up. Some cluster resources of the same type and name already existed. For example, cluster resources under kube-system. When there is a resource conflict during the restoration, Velero will skip the restoration step. In fact, the restoration process is normal and the “skipped” logs can be ignored (you can analyze these logs as needed).
	![](https://main.qcloudimg.com/raw/36f2cc21cdf30d6f4ec0b04e5ecab0f9.png)




### Verifying migration result

1. Run the following command to verify the cluster resources of cluster B after the migration. You can find that the Pods and PVC resources in the “default” and “default2” namespaces have been successfully migrated as expected, as shown below:
![image-20201118173604915](https://main.qcloudimg.com/raw/57b9724a809ea73a699fc4c437da07b7.png)
2. Log in to the MinIO service in cluster B, and you can find that the images in the MinIO service are not lost, indicating that the persistent volume data has been successfully migrated as expected.
![](https://main.qcloudimg.com/raw/c42a59abebd5049c0f85c564bcbf03f2.png)
3. At this point, the migration of resources between TKE clusters has been completed.
    After the migration is completed, run the following command to restore the backup storage locations of cluster A and cluster B to read/write mode, so that the next backup task can be performed normally, as shown below:
```bash
kubectl patch backupstoragelocation default --namespace velero \
   --type merge \
   --patch '{"spec":{"accessMode":"ReadWrite"}}'
```



## Summary

This document mainly introduces the principle, notes and operation methods of using Velero to migrate cluster resources among TKE clusters. The cluster resources in cluster A are successfully migrated seamlessly to cluster B. The whole migration process is simple and fast, and it is a very friendly cluster resource migration solution.

