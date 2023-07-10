## Overview

[Tencent Kubernetes Engine (TKE)](https://intl.cloud.tencent.com/product/tke) is a container management service with high scalability and performance. It provides a variety of application release methods and continuous delivery capabilities and supports microservice architectures. It can solve environment-related issues in the process of development, testing, and OPS and help you reduce costs and improve efficiency.

Businesses using containers usually involve shared access by multiple containers to a high number of configuration files, model files, log data, and attachments in such scenarios as business application deployment, DevOps, machine learning, and auto-scaling. Especially, in scenarios like machine learning, intelligent recommendation, and log data processing, in addition to basic data sharing, shared storage is also required to provide services that feature high throughput, high IOPS, and low latency and can sustain high concurrent requests. CFS can provide such services after simple configuration and mount to containers, making it particularly suitable for use in conjunction with TKE. This document describes how to use CFS on TKE.

## Prerequisites
You have already created a TKE cluster. If you haven't done so, please create one first as instructed in [Deploying TKE](https://intl.cloud.tencent.com/document/product/457/11741).



## Applying for CFS Resources and Getting Mount Point IP

- If you do not have a file system, please create one as instructed in [Creating File Systems and Mount Points](https://intl.cloud.tencent.com/document/product/582/9132). Please make sure that the VPC you select when creating the file system is the same as that of your TKE master to ensure network interconnectivity. 
- If you already have a file system in the same VPC as your TKE instance, you can enter the "[File System Details](https://console.cloud.tencent.com/cfs/fs)" page to get the mount point IP.

## Configuring CFS File System Mounting

#### Step 1. Start the NFS client on the node

Before mounting, please make sure that `nfs-utils` or `nfs-common` has already been installed in the system. The installation method is as follows:

- CentOS
```plaintext
sudo yum install nfs-utils
```
- Ubuntu 
```plaintext
sudo apt-get install nfs-common
```

#### Step 2. Create a PV
Run the following command to create a PesistentVolume (PV) of CFS type.
```plaintext
apiVersion: v1
kind: PersistentVolume
metadata:
  name: cfs
spec:
  capacity:
    storage: 10Gi
  volumeMode: Filesystem
  accessModes:
    - ReadWriteMany
  persistentVolumeReclaimPolicy: Retain
  mountOptions:
    - hard
    - nfsvers=4
  nfs:
    path: /
    server: 10.0.1.41
```
>?
> - nfs.server: mount point IP of the CFS file system obtained above. The file system IP is 10.0.1.41 in this example.
> - nfs.path: root directory or subdirectory of the CFS file system. The root directory is used in this example.
>


#### Step 3. Create a PVC
Then, create a PersistentVolumeClaim (PVC) and bind it to the PV.

```plaintext
kind: PersistentVolumeClaim
apiVersion: v1
metadata:
   name: cfsclaim
spec:
   accessModes:
		   - ReadWriteMany
   volumeMode: Filesystem
   storageClassName: ""
   resources:
     requests:
       storage: 10Gi
```

#### Step 4. Create a pod
Create a pod to declare that this volume is used for mounting.

```plaintext
kind: Pod
apiVersion: v1
metadata:
  name: mypod
spec:
  containers:
    - name: myfrontend
      image: nginx
      volumeMounts:
      - mountPath: "/var/www/html"
        name: mypd
  volumes:
    - name: mypd
      persistentVolumeClaim:
        claimName: cfsclaim
```
After the above steps are completed, you can use the file system in the newly created pod.

