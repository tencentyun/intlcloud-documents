## Overview

You can mount a CFS Turbo storage for an EKS cluster. The add-on is used to mount a Tencent Cloud CFS Turbo file system to a workload based on a proprietary protocol. Currently, only static configuration is supported. For more information about CFS storage types, see [Storage Types and Performance](https://intl.cloud.tencent.com/document/product/582/33745). 

## Prerequisites

An EKS cluster of v1.14 or later has been created. 

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
  storageClassName: ""
```

Parameter description:  
- **metadata.name**: the name of the created PV. 
- **spec.csi.volumeHandle**: it must be consistent with the PV name.  
- **spec.csi.volumeAttributes.host**: the IP address of the file system. You can check it in the information about the file system mount target.  
- **spec.csi.volumeAttributes.fsid**: fsid of the file system (not the file system ID). You can check it in the information about the file system mount target. It is the string after "tcp0:/" and before "/cfs" in the mount command, as shown below. 


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
- **metadata.name**: the name of the created PVC. 
- **spec.volumeName**: it must be consistent with the name of the PV created in [Step 1](#step1). 

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

