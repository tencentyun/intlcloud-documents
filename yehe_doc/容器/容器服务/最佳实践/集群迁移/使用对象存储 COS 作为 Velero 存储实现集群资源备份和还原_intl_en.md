## Overview


[Velero](https://velero.io/) (the previous version is called Heptio Ark), an open-source tool, can safely back up and restore, perform disaster recovery, and migrate Kubernetes cluster resources and persistent volumes. Deploying Velero in the TKE cluster or self-built Kubenetes cluster can achieve the following features:
- Back up cluster resources and restore in case of loss.
- Migrate cluster resources to other clusters.
- Replicate the production cluster resources to the development and test clusters.

Working principles of Velero is shown in the figure below (from [Velero](https://velero.io/) official website). When the user runs the backup command, the backup process is described as follows:
1. Call the custom resource API to create a backup object, as shown in (1).
2. When BackupController detects the generated backup object, as shown in (2), it executes the backup operation, as shown in (3).
3. Upload and store the backup cluster resources and storage volume snapshots to Velero's backend, as shown in (4) and (5).
![backup-process](https://main.qcloudimg.com/raw/1aea8598f3c0345101e91b586544896d.png)

In addition, when performing a restoration operation, Velero will synchronize the data of the specified backup object from the backend storage to the Kubernetes cluster.
For more information about Velero, see [Velero](https://velero.io/) official document. This document describes how to use [COS](https://intl.cloud.tencent.com/document/product/436) as the Velero backend storage to implement cluster backup and restoration.



## Prerequisites

- You have registered a [Tencent Cloud account](https://intl.cloud.tencent.com/register).
- Activate the [COS](https://console.cloud.tencent.com/cos5) service.
- Create a Kubernetes cluster of v1.10 or later version, and the cluster can use DNS and Internet services normally. For more information, see [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/30637).


## Directions
### Configuring COS

#### Creating a bucket

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5) to create a bucket for Velero to store backups. For more information, see [Creating Buckets](https://intl.cloud.tencent.com/document/product/436/13309).
2. [Set Access Permission](https://intl.cloud.tencent.com/document/product/436/13315) for the bucket. COS supports two permission types:
	- **Public permissions**: for the sake of security, the permission of private read/write is recommended for the bucket. For more information, see **Types of Permission** under [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312).
	- **User permissions**: the root account has all bucket permissions (full control) by default. You can add sub-accounts and grant them permissions including read/write, read/write ACL, and even **full control**.
	The sample sub-account has been granted the permissions of read/write for performing read/write on the bucket, as shown in the figure below:
	![](https://main.qcloudimg.com/raw/b26d331b8a3c65180b6ff3a540b3de24.png)



#### Obtaining the bucket access credentials

Velero uses an API compatible with AWS S3 to access COS. It needs to use a pair of access key ID and a signature created by the key for authentication. In the S3 API parameters:
- `access_key_id`: access key ID 
- `secret_access_key`: key


1. Log in to [CAM console](https://console.cloud.tencent.com/cam/capi) to create and obtain the keys `SecretId` and `SecretKey` of the COS authorized sub-account. Among them:
 -  The value of `SecretId` corresponds to the `access_key_id` field.
 -  The value of `SecretKey` corresponds to the `secret_access_key` field.
2. <span id="credentials"></span>According to the above corresponding relationship, create the credential configuration file `credentials-velero` required by Velero in the local directory. The content is as follows:
```bash
[default]
aws_access_key_id=<SecretId>
aws_secret_access_key=<SecretKey>
```



### Installing Velero 

1. Download the latest version of [Velero](https://github.com/vmware-tanzu/velero/releases) to the cluster environment. This document uses Velero v1.5.2 as an example, as shown below:
```bash
wget https://github.com/vmware-tanzu/velero/releases/download/v1.5.2/velero-v1.5.2-linux-amd64.tar.gz
```
2. Run the following command to decompress the installation package. The installation package provides Velero command lines and some sample files, as shown below:
```bash
tar -xvf velero-v1.5.2-linux-amd64.tar.gz
```
3. Run the following command to migrate the Velero executable file from the decompressed directory to the system environment variable directory for direct use. This document takes the migration to the `/usr/bin` directory as an example, as shown below:
```bash
mv velero-v1.5.2-linux-amd64/velero /usr/bin/
```
4. Run the following commands to install Velero, create Velero and Restic workloads and other necessary resource objects (for installation parameter descriptions, please see [table below](#velero)), as shown below:
```plaintext
velero install  --provider aws --plugins velero/velero-plugin-for-aws:v1.1.0 --bucket  <BucketName> \
--secret-file ./credentials-velero \
--use-restic \
--default-volumes-to-restic \
--backup-location-config \
region=ap-guangzhou,s3ForcePathStyle="true",s3Url=https://cos.ap-guangzhou.myqcloud.com
```
<span id="velero"></span>Installation parameter description:
<table>
<thead>
<tr>
<th  nowrap="nowrap">Parameter</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>--provider</td>
<td>Declare to use the plugin type provided by <code>aws</code>.</td>
</tr>
<tr>
<td>--plugins</td>
<td>Use AWS S3 compatible API plugin "velero-plugin-for-aws".</td>
</tr>
<tr>
<td>--bucket</td>
<td>The name of the bucket created in COS</td>
</tr>
<tr>
<td>--secret-file</td>
<td>The access credential file for accessing COS. For more information, see "<a href="#credentials">credentials-velero</a>" credential file created above.</td>
</tr>
<tr>
<td>--use-restic</td>
<td>Velero supports using the free and open-source backup tool <a href="https://github.com/restic/restic">Restic</a> to back up and restore Kubernetes storage volume data (<code>hostPath</code> volume is not supported, For more information, see <a href="https://velero.io/docs/v1.5/restic/#limitations">Restic Limitations</a>). It is recommended to enable this integration, which is a supplement to Velero's backup feature.</td>
</tr>
<tr>
<td  nowrap="nowrap">--default-volumes-to-restic</td>
<td>Enable Restic to back up all Pod volumes, provided that the <code>--use-restic</code> parameter is enabled.</td>
</tr>
<tr>
<td  nowrap="nowrap">--backup-location-config</td>
<td>Back up bucket access related configuration, including region, s3ForcePathStyle, s3Url, etc.</td>
</tr>
<tr>
<td>region</td>
<td>COS bucket region is compatible with S3 API, for example, the creation region is Guangzhou, and the value of parameter “region” is "ap-guangzhou".</td>
</tr>
<tr>
<td>s3ForcePathStyle</td>
<td>Use S3 file path format.</td>
</tr>
<tr>
<td>s3Url</td>
<td>S3 API access address compatible with COS. Please note that the domain name in the access address is not the public domain name used to create the COS bucket. It must be a URL in the format https://cos.&lt;region&gt;.myqcloud.com. For example, if the region is Guangzhou, then The parameter value is <code>https://cos.ap-guangzhou.myqcloud.com</code>.</td>
</tr>
</tbody></table>

You can use the command `velero install --help` to view other installation parameters. For example, if you do not need to back up storage volume data, you can set `--use-volume-snapshots=false` to disable storage volume snapshot backup.
Check the installation process after executing the installation command, as shown in the figure below:
![](https://main.qcloudimg.com/raw/817541d26a0d167de0a20a0f8127c8d1.png)

5. After the installation, wait for Velero and Restic workloads to be ready. Run the following command to check whether the configured storage location is available. If "Available" is displayed, it means that the cluster can access the COS normally, as shown in the figure below:
![](https://main.qcloudimg.com/raw/a1cf8fc3d5bd53daa09be30edac332fa.png)
At this point, the Velero installation is complete. For more information about Velero installation, see [Velero](https://velero.io/docs/) documentation on the official website.



### Velero backup and restoration testing

1. Use the Helm tool in the cluster to create a MinIO test service with persistent volumes. For the MinIO installation method, see [MinIO Installation](https://github.com/minio/charts). In this example, the MinIO service has bound a load balancer. You can use the public network address to access the management page in the browser.
![](https://main.qcloudimg.com/raw/9352391a728698fe72ca414fb55d03d1.png)
2. Log in to the MinIO Web management page and upload the image for testing, as shown in the figure below:
![](https://main.qcloudimg.com/raw/9dd7e1f08709292e5c58f5744ffb5f10.png)
3. <span id="velerostep3"></span>Using Velero backup, you can directly back up all objects in the cluster, or filter objects by type, namespace, / or tag. You can run the following command to only backup all resources in the default namespace, as shown below:
```bash
velero backup create default-backup --include-namespaces default
```
4. Run the following command to check whether the backup task is completed. When the status of the backup task is "Completed" and "ERRORS" is 0, it means that the backup task is completed without any errors.
```bash
velero backup get
```
	The backup process is shown in the figure below:
	![](https://main.qcloudimg.com/raw/fff36d963fb9b600e3c34c0556c5a2bf.png)
5. Run the following command to delete all resources under MinIO, including PVC persistent volumes, as shown below:
![](https://main.qcloudimg.com/raw/23a84feb0f24b45484175278c97c01b9.png)
6. After deleting the MinIO resource, you can use the previous backup to test whether the deleted MinIO resource can be successfully restored. Run the following command to temporarily update the backup storage location to read-only mode (to prevent Velero from creating or deleting backup objects in the backup storage location during the restoration process).
```bash
kubectl patch backupstoragelocation default --namespace velero \
			--type merge \
			--patch '{"spec":{"accessMode":"ReadOnly"}}'
```
	The execution process is shown in the figure below:
	![](https://main.qcloudimg.com/raw/8abb88e5ce2586dc6f3c0d268883e4cd.png)
7. Run the following command to create a restoration task using the backup "default-backup" created by Velero in [Step 3](#velerostep3) above, as shown below:
```bash
velero restore create --from-backup default-backup
```
	Use the command `velero restore get` to view the status of the restoration task. If the restoration status is "Completed" and "ERRORS" is 0, it means that the restoration task is completed, as shown in the figure below:
	![](https://main.qcloudimg.com/raw/ed52f0465d7bc59ce871678448961bd7.png)
8. After the restoration, run the following command. You can find that the related resources of the previously deleted MinIO have been restored successfully, as shown below:
![](https://main.qcloudimg.com/raw/fc58c6f4325913d01cd7bb131a920d78.png)
9. Log in to the MinIO management page on the browser. You can find the previously uploaded image, indicating that the data of the persistent volume is restored successfully, as shown below:
>!This document describes how to use Restic to backup and restore persistent volumes, but Restic does not support `hostPath` type volumes. For more information, see [Restic Limitations](https://velero.io/docs/v1.5/restic/#limitations).

![](https://main.qcloudimg.com/raw/1ed0a87a01ece26311c41a026cc8013a.png)
10. In addition, after the restoration, you can run the following command to restore the backup storage location to read/write mode, so that you can back up normally next time, as shown below:
```bash
kubectl patch backupstoragelocation default --namespace velero \
			--type merge \
			--patch '{"spec":{"accessMode":"ReadWrite"}}'
```



### Uninstalling Velero

Run the following command to uninstall Velero in the cluster, as shown below:
```bash
kubectl delete namespace/velero clusterrolebinding/velero
kubectl delete crds -l component=velero
```



## Summary

This document mainly introduces Velero, a Kubernetes cluster resource backup tool, and shows how to configure COS as Velero's backend storage, and successfully practices the backup and restoration operations of MinIO service resources and data.



## References

- [Velero Official Website](https://velero.io/)
- [Restic Introduction](https://github.com/restic/restic)
- [Restic Limitations](https://velero.io/docs/v1.5/restic/#limitations)
