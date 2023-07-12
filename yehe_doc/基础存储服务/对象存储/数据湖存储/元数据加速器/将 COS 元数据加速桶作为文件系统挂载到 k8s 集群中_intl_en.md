## Overview

Container Storage Interface (CSI) was developed by Kubernetes, Docker, and other communities as a standard for exposing file systems or block storage to containerized workloads on Container Orchestration Systems (COs) like Kubernetes.

The Kubernetes-csi-tencentcloud CHDFS plugin implements the CSI interface to make COS metadata acceleration-enabled buckets available to Kubernetes as a file system. You can quickly use COS metadata acceleration-enabled buckets in a container cluster with standard native Kubernetes in the form of CHDFS-FUSE. For more information, see [CHDFS-FUSE tool introduction](https://github.com/tencentyun/chdfs-fuse). The CHDFS-FUSE plugin allows you to mount COS metadata acceleration-enabled buckets to the corresponding workloads. It currently only supports the **Static Provisioning** mode (i.e., create a pv for an existing metadata acceleration-enabled bucket and create a corresponding pvc to use it).


## Environment Preparations

- Prepare a cluster with a **Kubernetes version 1.14 or later**. A [Tencent Kubernetes Engine (TKE) cluster](https://intl.cloud.tencent.com/document/product/457/40029) is recommended.
- For a metadata acceleration-enabled bucket, click **Performance Configuration > HDFS User Configuration** to configure the VPC for the Kubernetes cluster.


## How to Use

### Downloading the plugin

[Go to GitHub to download the plugin](https://github.com/TencentCloud/kubernetes-csi-tencentcloud) and install the Kubernetes-csi-tencentcloud CHDFS plugin in the cluster.

### Deploying the plugin

1. Deploy the CHDFS plugin.

 - If the Kubernetes version of the cluster is 1.20 or later, run the following commands:
```shell
kubectl apply -f  deploy/chdfs/kubernetes/csidriver-new.yaml
kubectl apply -f  deploy/chdfs/kubernetes/csi-node-rbac.yaml
kubectl apply -f  deploy/chdfs/kubernetes/csi-node.yaml
```
 - If the Kubernetes version of the cluster is earlier than 1.20, run the following commands:
```shell
kubectl apply -f  deploy/chdfs/kubernetes/csidriver-old.yaml
kubectl apply -f  deploy/chdfs/kubernetes/csi-node-rbac.yaml
kubectl apply -f  deploy/chdfs/kubernetes/csi-node.yaml
```

2. Run the following command to check whether the plugin status is Running:
```shell
kubectl get po -n kube-system | grep chdfs
csi-chdfs-node-fcwd4                 2/2     Running   0          23m
```

### Using the plugin

1. Edit the plugin configuration.
```shell
vim ./deploy/chdfs/examples/pv.yaml 
```
```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: csi-chdfs-pv
spec:
  accessModes:
  - ReadWriteMany
  capacity:
    storage: 10Gi
  csi:
    driver: com.tencent.cloud.csi.chdfs
    # Specify a unique volumeHandle, such as a pv name or file system ID
    volumeHandle: csi-chdfs-pv
    volumeAttributes:
      # Specify whether to allow access by other users. Valid values: true, false
      allowother: "true"
      # Specify whether to synchronize any memory changes to CHDFS in real time. Valid values: true, false
      sync: "false"
      # Specify whether to show the details of calling the fuse API. Valid values: true, false
      debug: "true"
      # Specify the mount address of the CHDFS mount point. An example value is cosn-test-1250000000.chdfs.ap-guangzhou.myqcloud.com
      url: "cosn-test-1250000000.chdfs.ap-guangzhou.myqcloud.com"
      # Additional args.
      additional_args: ""
  storageClassName: ""
~                       
```
Parameter description:

 - **allowother**: Specifies whether to allow access by other users.
 - **sync**: Specifies whether to synchronize any memory changes to the metadata acceleration-enabled bucket in real time.
 - **debug**: Specifies whether to show the details of calling the fuse API in logs.
 - **url**: Enter the correct bucket name and region. An example value is `cosn-test-1250000000.chdfs.ap-guangzhou.myqcloud.com`.
 - **additional_args**: CHDFS supports custom mount parameters. Separate two parameters with a space, such as `client.renew-session-lease-time-sec=100 cache.read.read-ahead-block-num=100`. Supported parameters are detailed as below:

| Parameter                                | Default Value      | Description                                                         |
| ----------------------------------- | ----------- | ------------------------------------------------------------ |
| security.ssl-ca-path                | -           | CA path, such as `/etc/ssl/certs/ca-bundle.crt`                   |
| client.renew-session-lease-time-sec | 10          | Session lease time, in seconds                                            |
| client.mount-sub-dir                | Root directory      | Subdirectory for mounting                                                  |
| client.user                         | Current username  | Username                                                      |
| client.group                        | Current group name    | Group name                                                         |
| client.force-sync                   | false       | Whether to force sync. This parameter is independent of "-o sync"                             |
| cache.update-sts-time-sec           | 30          | Update interval of data read/write temporary key, in seconds                                |
| cache.cos-client-timeout-sec        | 5           | Data upload/download timeout period, in seconds                                   |
| cache.inode-attr-expired-time-sec   | 30          | Cache expiration time of the inode attribute, in seconds                                  |
| cache.read.block-expired-time-sec   | 10          | [Read] Expiration time (seconds) for cache read on a single file descriptor (fd) (block-level)        |
| cache.read.max-block-num            | 256         | [Read] Maximum number of blocks for cache read on a single fd                    |
| cache.read.read-ahead-block-num     | 15          | [Read] Number of read-ahead blocks for a single fd (read-ahead-block-num < max-block-num) |
| cache.read.max-cos-load-qps         | 1024        | [Read] Maximum data download QPS for multiple fds (QPS * 1 MB < ENI bandwidth)     |
| cache.read.load-thread-num          | 128         | [Read] Number of workers for data download on multiple fds                         |
| cache.read.select-thread-num        | 64          | [Read] Number of workers for metadata query on multiple fds                       |
| cache.read.rand-read                | false       | [Read] Whether to enable random read                                     |
| cache.write.max-mem-table-range-num | 32          | [Write] Maximum number of range for caching the current data of a single fd                |
| cache.write.max-mem-table-size-mb   | 64          | [Write] Maximum capacity (MB) for caching the current data of a single fd                 |
| cache.write.max-cos-flush-qps       | 256         | [Write] Maximum data upload QPS for multiple fds (QPS * 4 MB < ENI bandwidth)     |
| cache.write.flush-thread-num        | 128         | [Write] Number of workers for data upload on multiple fds                         |
| cache.write.commit-queue-len        | 100         | [Write] Length of the queue for committing the metadata of a single fd                           |
| cache.write.max-commit-heap-size    | 500         | [Write] Maximum capacity for committing the metadata of a single fd. This parameter does not need to be set               |
| cache.write.auto-merge              | true        | [Write] Whether to automatically merge incomplete multiparts when writing to a single fd                     |
| cache.write.auto-sync               | false       | [Write] Whether to automatically flush dirty pages when writing to a single fd
| cache.write.auto-sync-time-ms       | 1000        | [Write] Interval (ms) for automatic dirty page flushing when writing to a single fd          |
| log.level                           | info        | Log level                                                     |
| log.file.filename                   | default.log | Log filename                                                  |
| log.file.log-rotate                 | true        | Whether to enable log rotation                                                     |
| log.file.max-size                   | -           | Maximum size of a log file, in MB                                   |
| log.file.max-days                   | -           | Maximum retention days of a log file                               |
| log.file.max-backups                | -           | Maximum number of historical log files                                     |


2. Run the following command to create a pv:
```shell
# Among the parameters supported by pv, only url is a required parameter
kubectl apply -f deploy/chdfs/examples/pv.yaml
```

3. Run the following command to create a pvc:
```shell
kubectl apply -f deploy/chdfs/examples/pvc.yaml
```

4. Run the following command to check whether the pvc and pv are bound:
```
kubectl get pvc csi-chdfs-pvc
```
![image-20230215194533905](https://qcloudimg.tencent-cloud.cn/raw/74be024c61300613f121fff42cf78819.png)

5. Run the following command to create a pod:
```shell
kubectl apply -f deploy/chdfs/examples/pod.yaml
```

6. Run the following command to check whether the pod status is Running:
```shell
kubectl get pod
```
![image-20230215194533905](https://qcloudimg.tencent-cloud.cn/raw/73490942b3d21731e140f9c071a6393f.png)

7. Check the file system status. If the information similar to the following is displayed, the file system has been mounted:
```shell
df -h 
```
![image-20230215211144396](https://qcloudimg.tencent-cloud.cn/raw/afd113649d54e28c59f54c4943ea73a2.png)
