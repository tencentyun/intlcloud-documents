## Overview

### Volume Types
- **Host path**: Mount container-located host's file directory to specified container path (corresponding to HostPath in Kubernetes). You can choose not to set the source path (corresponding to EmptyDir in Kubernetes) based on your business needs. If you do not set the source path, the system will mount the temporary directory of the assigned host to the mount point of the container. **A local disk volume with specified source path is well suited for durably storing data to container-located host, while EmptyDir is well suited for temporarily storing container.**
- **NFS disk**: Simply enter the NFS path. You can use Tencent Cloud's [Cloud File Storage](https://intl.cloud.tencent.com/document/product/582/9127) or self-built NFS file storage. **An NFS volume is suitable for persistent storage with frequent reads and writes and scenarios such as big data analytics, media processing, and content management.**
- **Existing PersistentVolumeClaim**: Use an existing PersistentVolumeClaim to declare the storage of the workload, which automatically assigns or creates a PersistentVolume to mount to the corresponding Pod. This is mainly suitable for stateful applications created by StatefulSets. For more information, see [PV and PVC Management](https://intl.cloud.tencent.com/document/product/457/30679).
- **New PersistentVolumeClaim**: Create a PersistentVolumeClaim to declare the storage of the workload, which automatically assigns or creates a PersistentVolume to mount to the corresponding Pod. This is mainly suitable for stateful applications created by StatefulSets. For more information, see [PV and PVC Management](https://intl.cloud.tencent.com/document/product/457/30679).
- **CBS**: Use Tencent Cloud's CBS-based Kubernetes block storage plugin. You can specify a CBS cloud disk to be mounted to a path in the container. When the container is migrated, the cloud disk will be migrated too. **A CBS volume is suitable for persistent storage of data in stateful services such as MySQL. For a service for which a CBS volume is set, the maximum number of Pods is 1.**
- **ConfigMap**: Mount a ConfigMap to the Pod as a file system. You can customize the ConfigMap entries to be mounted to the specified path. For more information, see [ConfigMap Management](https://intl.cloud.tencent.com/document/product/457/30675).
- **Secret**: Mount a Secret to the Pod as a file system. You can customize the Secret entries to be mounted to the specified path. For more information, see [Secret Management](https://intl.cloud.tencent.com/document/product/457/30676).


### Notes on Volumes

- After creating a volume, you need to set the mount point of the container.
- Under the same service, the name of the volume and the mount point set for the container must be unique.
- When the source path of a local disk volume is empty, the system will assign a temporary directory `/var/lib/kubelet/pods/pod_name/volumes/kubernetes.io~empty-dir`, and the volume using the temporary directory is the same as that of the Pod.
- If no permission is set for volume mount, the default setting will be read/write permission.

## Operation Guide for Volumes in the Console

### Creating a Workload to Mount a Volume

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **Clusters** to go to the cluster management page.
3. Click the ID of the cluster where workload needs to be deployed to enter the cluster management page.
4. Under "Workload", select a workload type to go to the corresponding information page. For example, select "Workload" > "DaemonSet" to go to the DaemonSet information page. See the figure below:
![](https://main.qcloudimg.com/raw/66d7b437dfd4ed9ae0b8796f1f898f36.png)
5. Click **Create** to go to the "Create a workload" page.
6. Set the workload name, namespace and other information as instructed. In "Volume", click **Add a volume** to add a volume. See the figure below:
![Add a volume](https://main.qcloudimg.com/raw/cb585f7e821d44170941dda705414b0d.png)
7. Select the storage method of the volume and configure the mount point based on actual needs.
9. Click **Create a workload** to complete the creation.

## Using kubectl to Manipulate Volumes

The following is a sample where which you can perform creation directly using kubectl.

### Sample YAML for Mounting a Volume to a Pod
```Yaml
apiVersion: v1
kind: Pod
metadata:
  name: test-pd
spec:
  containers:
  - image: k8s.gcr.io/test-webserver
    name: test-container
    volumeMounts:
    - mountPath: /cache
      name: cache-volume
  volumes:
  - name: cache-volume
    emptyDir: {}
```
- spec.volumes: Set the name, type, and parameters of the volume.
  - spec.volumes.emptyDir: Set the temporary path.
  - spec.volumes.hostPath: Set the host path.
  - spec.volumes.nfs: Set the NFS disk.
  - spec.volumes.persistentVolumeClaim: Set the existing PersistentVolumeClaim.
- spec.volumeClaimTemplates: If this declaration is used, PersistentVolumeClaim and PersistentVolume will be automatically created based on the content.
- spec.containers.volumeMounts: Enter the mount point of the volume.
