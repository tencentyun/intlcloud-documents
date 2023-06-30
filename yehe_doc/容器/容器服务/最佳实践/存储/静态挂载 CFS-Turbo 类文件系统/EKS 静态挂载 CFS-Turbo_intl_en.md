## Overview

You can mount a CFS Turbo storage for an EKS cluster. The add-on is used to mount a Tencent Cloud CFS Turbo file system to a workload based on a proprietary protocol. Currently, only static configuration is supported. For more information about CFS storage types, see [Storage Types and Performance](https://intl.cloud.tencent.com/document/product/582/33745). 

## Prerequisites

You have created an EKS cluster of v1.14 or later version. 

## Directions 

### Creating a file system

Create a CFS Turbo file system. For details, see [Creating File Systems and Mount Targets](https://intl.cloud.tencent.com/document/product/582/9132). 

>! After the file system is created, you need to associate the cluster network (vpc-xx) with the [CCN instance](https://intl.cloud.tencent.com/document/product/1003/30064) of the file system. You can check it in the information about the file system mount target. 
>

### Deploying a Node Plugin

#### Step 1. Create a csidriver.yaml file
Here is an example of a csidriver.yaml file:
```yaml
apiVersion: storage.k8s.io/v1beta1
kind: CSIDriver
metadata:
  name: com.tencent.cloud.csi.cfsturbo
spec:
  attachRequired: false
  podInfoOnMount: false
```

#### Step 2. Create a CSI driver
Run the following command to create a CSI driver:
```sh
kubectl apply -f csidriver.yaml
```

### Creating a CFS Turbo volume

#### Step 1. Create a CFS Turbo type PV based on the following template[](id:step1)

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-cfsturbo
spec:
  accessModes:
  - ReadWriteMany
  capacity:
    storage: 10Gi
  csi:
    driver: com.tencent.cloud.csi.cfsturbo
    volumeHandle: pv-cfsturbo
    volumeAttributes: 
      host: *.*.*.*
      fsid: ********
      # cfs turbo subPath
      path: /
  storageClassName: ""
```

Parameter description:  
- **metadata.name**: The name of the created PV. 
- **spec.csi.volumeHandle**: It must be consistent with the PV name.  
- **spec.csi.volumeAttributes.host**: The IP address of the file system. You can check it in the file system mount target information.  
- **spec.csi.volumeAttributes.fsid**: The fsid of the file system (not the file system ID). You can check it in the file system mount target information. It is the string between "tcp0:/" and "/cfs" in the mount command, as shown in the following figure. 
- **spec.csi.volumeAttributes.path**: The subdirectory of the file system. “/” is entered if it is left empty (to improve the mounting performance, “/” is located under “/cfs directory”). If you want to specify a subdirectory for mounting, you must ensure that the subdirectory exists in “/cfs” in the file system. The workload cannot access the parent directory of the subdirectory after mounting. For example, for “path: /test”, you must ensure that the “/cfs/test” exists in the file system.
![](https://qcloudimg.tencent-cloud.cn/raw/653a12c669d45b112f994e2f1f867abf.png)

#### Step 2. Create a PVC that is bound to the PV based on the following template

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pvc-cfsturbo
spec:
  storageClassName: ""
  volumeName: pv-cfsturbo
  accessModes:
  - ReadWriteMany
  resources:
    requests:
      storage: 10Gi
```

Parameter description:  
- **metadata.name**: The name of the created PVC. 
- **spec.volumeName**: It must be consistent with the name of the PV created in [Step 1](#step1). 

### Using a CFS Turbo volume

Create a Pod that mounts the PVC based on the following template. 

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx 
spec:
  containers:
  - image: ccr.ccs.tencentyun.com/qcloud/nginx:1.9
    imagePullPolicy: Always
    name: nginx
    ports:
    - containerPort: 80
      protocol: TCP
    volumeMounts:
      - mountPath: /var/www
        name: data
  volumes:
  - name: data
    persistentVolumeClaim:
      claimName: pvc-cfsturbo
```

