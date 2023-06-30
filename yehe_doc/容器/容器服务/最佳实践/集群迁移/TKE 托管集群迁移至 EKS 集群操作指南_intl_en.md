

## Prerequisites
- A TKE managed cluster on v1.18 or later (cluster A) exists.
- A target EKS cluster (cluster B) on v1.20 or later has been created. For how to create an EKS cluster, see [Connecting to a Cluster](https://intl.cloud.tencent.com/document/product/457/34048).
- Both clusters A and B share the same COS bucket as Velero backend storage. For how to configure a COS bucket, see [Using COS as Velero Storage to Implement Backup and Restoration of Cluster Resources](https://intl.cloud.tencent.com/document/product/457/38939).
- We recommend that Clusters A and B be under the same VPC, so that you can back up data in the PVC.
- Make sure that image resources can be pulled properly after migration. For how to configure an image repository in an EKS cluster, see [Image Repository FAQs](https://intl.cloud.tencent.com/document/product/457/40028).
- Make sure that the Kubernetes versions of both clusters are compatible. We recommend you use the same version. If cluster A is on a lower version, upgrade it before migration.

## Migration Limitations

- After workloads with a fixed IP are enabled in a TKE cluster, their IPs will change after the migration to an EKS cluster.
- EKS clusters with containerd v1.4.3 as the container runtime are not compatible with images from Docker Registry v2.5 or earlier, or Harbor v1.10 or earlier.
- In an EKS cluster, each Pod comes with 20 GiB free temporary disk space for image storage by default, which is created and terminated along the lifecycle of the Pod.
- EKS doesn't support RDMA.
- EKS doesn't support kernel parameters starting with `net`.
- EKS doesn't support the deployment of DaemonSet type workloads.
- EKS doesn't support the deployment of NodePort type services.
- EKS Pods can't listen on port 9100 and ports above 62000.
- For more limitations, see <a href="https://intl.cloud.tencent.com/document/product/457/34050"> Notes</a>.

## Migration Directions
The following describes how to migrate resources from TKE cluster A to EKS cluster B.

### Configuring COS
For detailed directions, see [Using COS as Velero Storage to Implement Backup and Restoration of Cluster Resources](https://intl.cloud.tencent.com/document/product/457/38939).

### Downloading Velero
1. Download the latest version of [Velero](https://github.com/vmware-tanzu/velero/releases) to the cluster environment. Velero v1.8.1 is used as an example in this document.  
```bash
wget https://github.com/vmware-tanzu/velero/releases/download/v1.8.1/velero-v1.8.1-linux-amd64.tar.gz
```
2. Run the following command to decompress the installation package, which contains Velero command lines and some sample files.  
```bash
tar -xvf velero-v1.8.1-linux-amd64.tar.gz
```
3. Run the following command to migrate the Velero executable file from the decompressed directory to the system environment variable directory, that is, `/usr/bin` in this document, as shown below:
```bash
cp velero-v1.8.1-linux-amd64/velero /usr/bin/
```

### Installing Velero in clusters A and B

1. Configure the Velero client and enable CSI.
```bash
velero client config set features=EnableCSI
```
2. Run the following command to install Velero in clusters A and B and create Velero workloads as well as other necessary resource objects.
	- Below is an example of using CSI for PVC backup:
```plaintext
velero install  --provider aws  \
--plugins velero/velero-plugin-for-aws:v1.1.0,velero/velero-plugin-for-csi:v0.2.0 \
--features=EnableCSI \
--features=EnableAPIGroupVersions \
--bucket <BucketName> \
--secret-file ./credentials-velero \
--use-volume-snapshots=false \
--backup-location-config region=ap-guangzhou,s3ForcePathStyle="true",s3Url=https://cos.ap-guangzhou.myqcloud.com
```
>! EKS doesn't support DaemonSet deployment, so none of the samples in this document support the restic add-on.
>
	- If you don't need to back up the PVC, see the following installation sample:
```plaintext
./velero install  --provider aws --use-volume-snapshots=false --bucket gtest-1251707795  --plugins velero/velero-plugin-for-aws:v1.1.0   --secret-file ./credentials-velero  --backup-location-config region=ap-guangzhou,s3ForcePathStyle="true",s3Url=https://cos.ap-guangzhou.myqcloud.com
```
For installation parameters, see [Using COS as Velero Storage to Implement Backup and Restoration of Cluster Resources](https://intl.cloud.tencent.com/document/product/457/38939) or run the `velero install --help` command.
[](id:velero) Other installation parameters are as described below:
<table>
<thead>
<tr>
<th  nowrap="nowrap">Installation Parameter</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>--plugins</td>
<td>Use the AWS S3 API-compatible add-on `velero-plugin-for-aws`; use the CSI add-on <a href="https://github.com/vmware-tanzu/velero-plugin-for-csi/">velero-plugin-for-csi</a> to back up `csi-pv`. We recommend you enable it.</td>
</tr>
<tr>
<td>--features</td>
<td>Enable optional features:<a href="https://velero.io/docs/v1.8/enable-api-group-versions-feature/">Enable the API group version feature.</a> This feature is used for compatibility with different API group versions and we recommend you enable it.<a href="https://velero.io/docs/v1.8/csi/">Enable the CSI snapshot feature.</a> This feature is used to back up the CSI-supported PVC, so we recommend you enable it.</td>
</tr>
<tr>
<td>--use-restic</td>
<td>Velero supports the <a href="https://github.com/restic/restic">restic</a> open-source tool to back up and restore Kubernetes storage volume data (<code>hostPath</code> volumes are not supported. For details, see <a href="https://velero.io/docs/v1.5/restic/#limitations">here</a>). It's used to supplement the Velero backup feature. During the migration to an EKS cluster, enabling this parameter will fail the backup.</td>
</tr>
<tr>
<td>--use-volume-snapshots=false</td>
<td>Disable the default snapshot backup of storage volumes.</td>
</tr>
</tbody></table>
3. After the installation is complete, wait for the Velero workload to be ready. Run the following command to check whether the configured storage location is available. If `Available` is displayed, the cluster can access the COS bucket.
```bash
velero backup-location get
NAME      PROVIDER   BUCKET/PREFIX      PHASE       LAST VALIDATED                  ACCESS MODE   DEFAULT
default   aws        <BucketName>   Available     2022-03-24 21:00:05 +0800 CST      ReadWrite     true
```
At this point, you have completed the Velero installation. For more information, see [Velero Documentation](https://velero.io/docs/).

### (Optional) Installing `VolumeSnapshotClass` in clusters A and B
>? 
>- Skip this step if you don't need to back up the PVC.
>- For more information on storage snapshot, see [Backing up and Restoring PVC via CBS-CSI Add-on](https://intl.cloud.tencent.com/document/product/457/40003).

1. Make sure you have installed the [CBS-CSI add-on](https://github.com/TencentCloud/kubernetes-csi-tencentcloud/blob/master/docs/README_CBS.md).
2. Grant CBS snapshot permissions for `TKE_QCSRole` in the [CAM console](https://console.cloud.tencent.com/cam/role). For details, see [CBS-CSI](https://intl.cloud.tencent.com/document/product/457/39136).
3. Use the following YAML to create a `VolumeSnapshotClass` object as shown below:
```yaml
apiVersion: snapshot.storage.k8s.io/v1beta1
kind: VolumeSnapshotClass
metadata:
  labels:
    velero.io/csi-volumesnapshot-class: "true"
  name: cbs-snapclass
driver: com.tencent.cloud.csi.cbs
deletionPolicy: Delete
```
4. Run the following command to check whether the `VolumeSnapshotClass` has been created successfully as shown below:
```bash
$ kubectl get volumesnapshotclass
NAME            DRIVER                      DELETIONPOLICY   AGE
cbs-snapclass   com.tencent.cloud.csi.cbs   Delete           17m
```



### (Optional) Creating sample resource for cluster A

>? Skip this step if you don't need to back up the PVC.

Deploy a MinIO workload with the PVC in a Velero instance in cluster A. Here, the `cbs-csi` dynamic storage class is used to create the PVC and PV.
1. Use `provisioner` in the cluster to dynamically create the PV for the `com.tencent.cloud.csi.cbs` storage class. A sample PVC is as follows:
```bash
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  annotations:
    volume.beta.kubernetes.io/storage-provisioner: com.tencent.cloud.csi.cbs
  name: minio
spec:
  accessModes:
  - ReadWriteOnce
  resources:
    requests:
      storage: 10Gi
  storageClassName: cbs-csi
  volumeMode: Filesystem
```
2. Use the Helm tool to create a MinIO testing service that references the above PVC. For more information on MinIO installation, see [here](https://github.com/minio/charts). In this sample, a load balancer has been bound to the MinIO service, and you can access the management page by using a public network address.
![](https://qcloudimg.tencent-cloud.cn/raw/dec9aa32caf4ffb390bbb54b484aa3b5.png)
3. Log in to the MinIO web management page and upload the images for testing as shown below:
  ![](https://qcloudimg.tencent-cloud.cn/raw/f709be2542e9830116eaf03c77027e1c.png)

### Backup and restoration
1. To create a backup in cluster A, see [Creating a backup in cluster A](https://intl.cloud.tencent.com/document/product/457/38940) in the **Cluster Migration** directions.
2. To perform a restoration in cluster B, see [Performing a restoration in cluster B](https://intl.cloud.tencent.com/document/product/457/38940) in the **Cluster Migration** directions.
3. Verify the migration result:
	- If you don't need to back up the PVC, see [Verifying migration result](https://intl.cloud.tencent.com/document/product/457/38940) in the **Cluster Migration** directions.
	- If you need to back up the PVC, perform a verification as follows:
  1. Run the following command to verify the resources in cluster B after migration. You can see that the Pods, PVC, and Service have been successfully migrated as shown below:

    ![](https://qcloudimg.tencent-cloud.cn/raw/3bafcbd38e9a9c63ba7804a4773e9a9c.png)
  2. Log in to the MinIO service in cluster B. You can see that the images in the MinIO service are not lost, indicating that the persistent volume data has been successfully migrated as expected.

    ![](https://qcloudimg.tencent-cloud.cn/raw/f709be2542e9830116eaf03c77027e1c.png)
4. At this point, the migration of resources between TKE and EKS clusters has been completed.
    After the migration is complete, run the following command to restore the backup storage locations of clusters A and B to read/write mode as shown below, so that the next backup task can be performed normally:
  ```bash
  kubectl patch backupstoragelocation default --namespace velero \
     --type merge \
     --patch '{"spec":{"accessMode":"ReadWrite"}}'
  ```

## FAQs About EKS Usage
- Failed to pull an image: See [Image Repository FAQs](https://intl.cloud.tencent.com/document/product/457/40028).
- Failed to perform a DNS query: This type of failure often takes the form of failing to pull a Pod image or deliver logs to a self-built Kafka cluster. For more information, see [Customized DNS Service of Elastic Cluster](https://intl.cloud.tencent.com/document/product/457/44025).
- Failed to deliver logs to CLS: When you use an EKS cluster to deliver logs to CLS for the first time, you need to authorize the service as instructed in [Enabling Log Collection](https://intl.cloud.tencent.com/document/product/457/40950).
- By default, up to 100 Pods can be created for each cluster. If you need to create more, see [Notes on Pod Scheduled to Virtual Node](https://intl.cloud.tencent.com/document/product/457/39760#.E9.BB.98.E8.AE.A4.E9.85.8D.E9.A2.9D).
- When Pods are frequently terminated and recreated, the `Timeout to ensure pod sandbox` error is reported: The add-ons in EKS Pods communicate with the control plane for health checks. If the network remains disconnected for six minutes after Pod creation, the control plane will initiate the termination and recreation. In this case, you need to check whether the security group associated with the Pod has allowed access to the 169.254 route.
- Pod port access failure/not ready:
  - Check whether the service container port conflicts with the EKS control plane port as instructed in [Notes](https://intl.cloud.tencent.com/document/product/457/34050).
  - If the Pod can be pinged succeeded, but the telnet failed, check the security group.
- When creating an instance, you can use the following features to speed up image pull: [Mirror cache](https://intl.cloud.tencent.com/document/product/457/44484) and [Mirror reuse](https://intl.cloud.tencent.com/document/product/457/43136).
- Failed to dump business logs: After an EKS Job business exits, the underlying resources are repossessed, and container logs can't be viewed by using the `kubectl logs` command, adversely affecting debugging. You can dump the business logs by delaying the termination or setting the `terminationMessage` field as instructed in [How to set container's termination message?](https://intl.cloud.tencent.com/document/product/457/43136).
- The Pod restarts frequently, and the `ImageGCFailed` error is reported: An EKS Pod has 20 GiB disk size by default. If the disk usage reaches 80%, the EKS control plane will trigger the container image repossession process to try to repossess the unused images and free up the space. If it fails to free up any space, `ImageGCFailed: failed to garbage collect required amount of images` will be reported to remind you that the disk space is insufficient. Common causes of insufficient disk space include:
  - The business has a lot of temporary output.
  - The business holds deleted file descriptors, so some space is not freed up.

## References
- [Container Storage Interface Snapshot Support in Velero](https://velero.io/docs/v1.8/csi/)
- [Enable API Group Versions Feature](https://velero.io/docs/v1.8/enable-api-group-versions-feature/)
- [Installing MinIO from Marketplace](https://intl.cloud.tencent.com/document/product/457/37706)
