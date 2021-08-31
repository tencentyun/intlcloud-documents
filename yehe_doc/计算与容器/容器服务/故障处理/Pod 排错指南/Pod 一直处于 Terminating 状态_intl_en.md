This article describes the causes that lead to a Pod remaining in the Terminating status and how to troubleshoot these issues. Refer to the following instructions for troubleshooting.

## Possible Causes
- Insufficient disk space
- Files with the **i** attribute exist
- A bug in Docker version 17
- Finalizers exist
- A bug in earlier versions of kubelet list-watch
- Dockerd status and containerd status is not in sync
- A bug in Daemonset Controller

## Troubleshooting
### Checking if disk space is sufficient
If the disk where the Docker data directory resides is full, Docker will not function properly. It cannot even delete or create containers. Therefore it cannot respond to kubelet’s call to delete containers. Use `kubectl describe pod <pod-name>` to query event and get the following messages:
```bash
Normal  Killing  39s (x735 over 15h)  kubelet, 10.179.80.31  Killing container with id docker://apigateway:Need to kill Pod
```

For solutions and more information, see [Disk Full](https://intl.cloud.tencent.com/document/product/457/35753).

### Checking to see if files with the **i** attribute exist
#### Error description
Use `man chattr` to display a description of the **i** attribute, as shown below:
``` txt
       A file with the 'i' attribute cannot be modified: it cannot be deleted or renamed, no link can be created to this file and no data can be written to the file.  Only the superuser or a process possessing the CAP_LINUX_IMMUTABLE capability can set or clear this attribute.
```
> If the container image file itself or files stored in the container have the **i** attribute, they cannot be modified or deleted. 
>
When Pods are deleted, container directories are cleaned. If the directories have files that cannot be deleted, the directories cannot be deleted, which causes the Pods to remain in the Terminating status. In this case, kubelet displays the following error message:
``` log
Sep 27 14:37:21 VM_0_7_centos kubelet[14109]: E0927 14:37:21.922965   14109 remote_runtime.go:250] RemoveContainer "19d837c77a3c294052a99ff9347c520bc8acb7b8b9a9dc9fab281fc09df38257" from runtime service failed: rpc error: code = Unknown desc = failed to remove container "19d837c77a3c294052a99ff9347c520bc8acb7b8b9a9dc9fab281fc09df38257": Error response from daemon: container 19d837c77a3c294052a99ff9347c520bc8acb7b8b9a9dc9fab281fc09df38257: driver "overlay2" failed to remove root filesystem: remove /data/docker/overlay2/b1aea29c590aa9abda79f7cf3976422073fb3652757f0391db88534027546868/diff/usr/bin/bash: operation not permitted
Sep 27 14:37:21 VM_0_7_centos kubelet[14109]: E0927 14:37:21.923027   14109 kuberuntime_gc.go:126] Failed to remove container "19d837c77a3c294052a99ff9347c520bc8acb7b8b9a9dc9fab281fc09df38257": rpc error: code = Unknown desc = failed to remove container "19d837c77a3c294052a99ff9347c520bc8acb7b8b9a9dc9fab281fc09df38257": Error response from daemon: container 19d837c77a3c294052a99ff9347c520bc8acb7b8b9a9dc9fab281fc09df38257: driver "overlay2" failed to remove root filesystem: remove /data/docker/overlay2/b1aea29c590aa9abda79f7cf3976422073fb3652757f0391db88534027546868/diff/usr/bin/bash: operation not permitted
```

#### Solution
- Permanent solution: do not store files with the **i** attribute in container images or set a launched container with the **i** attribute.
- Temporary solution:
 1. Use the file path in the kubelet log and run the command `chattr -i <file>`, as shown below:
``` bash
    chattr -i /data/docker/overlay2/b1aea29c590aa9abda79f7cf3976422073fb3652757f0391db88534027546868/diff/usr/bin/bash
```
 2. Wait for kubelet to restart and try again. You can delete the Pod now.

### Checking for the bug in Docker Version 17
#### Error description
Docker hangs without any response. Running `kubectl describe pod <pod-name>` returns the following results:
```bash
Warning FailedSync 3m (x408 over 1h) kubelet, 10.179.80.31 error determining status: rpc error: code = DeadlineExceeded desc = context deadline exceeded
```

The cause is likely to be a bug in Docker version 17. You can use `kubectl -n cn-staging delete pod apigateway-6dc48bf8b6-clcwk –force –grace-period=0` to force delete the pod, but you can still see it using `docker ps`.

#### Solution
Upgrade Docker to version 18. Version 18 uses a new dockerd version and fixed many bugs.
- If the problem persists, [submit a ticket](https://console.cloud.tencent.com/workorder/category/?level1_id=6&level2_id=350&source=undefined&data_title=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1TKE&step=1) for further assistance. **We do not recommend that you force delete the pod** as this may impact your business.

### Checking for Finalizers
#### Error description
If a Kubernetes resource has the `finalizers` metadata, it is created by an application and the `finalizers` field contains an identifier of the application. For example, Rancher-created resources have the `finalizers` identifier.

To delete this type of resource, the application responsible must clean them up and remove the `finalizers` identifiers before they can be deleted.

#### Solution
Use `kubectl edit` to manually edit the resources to remove `finalizers` before deleting them.


### Check for a bug in an earlier version of kubelet list-watch
We discovered that, when you use Kubernetes v1.8.13, kubelet list-watch has a bug that prevents kubelet from receiving event information after deleting a Pod, which means the Pod is not truly deleted. This leads to the Pod remaining in the Terminating status.

Refer to [Updating Clusters](https://intl.cloud.tencent.com/document/product/457/30640) for instructions on how to update Kubernetes.

### Checking if dockerd and containerd are synchronized

#### Error description
If you use the AUFS storage driver and the disk is full, the kernel may panic and output the following error message:
``` txt
aufs au_opts_verify:1597:dockerd[5347]: dirperm1 breaks the protection by the permission bits on the lower branch
```
If this happens, it may lead to status synchronization issues, and dockerd logs may contain records similar to the following:
``` log
Sep 18 10:19:49 VM-1-33-ubuntu dockerd[4822]: time="2019-09-18T10:19:49.903943652+08:00" level=error msg="Failed to log msg \"\" for logger json-file: write /opt/docker/containers/54922ec8b1863bcc504f6dac41e40139047f7a84ff09175d2800100aaccbad1f/54922ec8b1863bcc504f6dac41e40139047f7a84ff09175d2800100aaccbad1f-json.log: no space left on device"
```

#### Analysis
You can use one of the following methods to find out if dockerd and containerd are in sync.
* Use `describe pod` to obtain the ID of the container. Then, use `docker ps` to query the status of the container and see if it matches the status from dockerd.
* Use `docker-container-ctr` to query the container status in containerd, as shown below:
``` bash
  $ docker-container-ctr --namespace moby --address /var/run/docker/containerd/docker-containerd.sock task ls |grep a9a1785b81343c3ad2093ad973f4f8e52dbf54823b8bb089886c8356d4036fe0
  a9a1785b81343c3ad2093ad973f4f8e52dbf54823b8bb089886c8356d4036fe0    30639    STOPPED
```

If the status of the container in containerd is `stopped` or empty and it is `running` in dockerd, then the container status is not synchronized between dockerd and containerd.




#### Solution
* Temporary solution: run `docker container prune` or restart dockerd.
* Permanent solution: use containerd instead of both containerd and dockerd to work around the bug in dockerd.

### Checking for the Daemonset Controller bug

Kubernetes 1.10 and 1.11 have a bug that causes Daemonset Pod to remain in the Terminating status. In this case, Daemonset Controller reuses the predicates logic of scheduler which sorts the nodeSelector array (passed as pointer parameters) from nodeAffinity. This results in spec being different from that stored by apiserver. At the same time, Daemonset Controller uses spec to calculate the hash of Daemonset for version control purposes.
This difference in parameter values causes the Pod to get stuck in a loop of launching and stopping.

#### Solution
- Temporary solution: make sure rollingUpdate Daemonset uses nodeSelector rather than nodeAffinity.
- Permanent solution: refer to [Updating Clusters](https://intl.cloud.tencent.com/document/product/457/30640) for instructions on how to update Kubernetes to 1.12.

