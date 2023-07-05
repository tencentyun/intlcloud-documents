

## Overview

You can mount a CFS Turbo storage for a TKE cluster by installing a `kubernetes-csi-tencentloud` add-on. This add-on is used to mount the Tencent Cloud CFS Turbo file system to a workload based on a private protocol. Currently, only static configuration is supported. For more information about CFS storage types, see [Storage Types and Performance](https://intl.cloud.tencent.com/document/product/582/33745).  

## Prerequisites

You have created a TKE cluster or created a Kubernetes cluster on Tencent Cloud, and the cluster version is 1.14 or later.  

## Directions

### Creating a file system[](id:create-cfs)

Create a CFS Turbo file system. For details, see [Creating File Systems and Mount Targets](https://intl.cloud.tencent.com/document/product/582/9132).  

>! After the file system is created, you need to associate the cluster network (vpc-xx) with the [CCN instance](https://intl.cloud.tencent.com/document/product/1003/30064) of the file system. You can check it in the information about the file system mount target.  


### Deploying a RBAC policy

If you want to mount a CFS Turbo volume, you need to run the `kubectl apply -f  csi-node-rbac.yaml` command to deploy a RBAC policy in the cluster. The following csi-node-rbac.yaml code is for your reference:

```yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: cfsturbo-csi-node-sa
  namespace: kube-system
---
kind: ClusterRole
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  name: cfsturbo-csi-node-role
rules:
  - apiGroups: [""]
    resources: ["persistentvolumes", "endpoints", "configmaps"]
    verbs: ["get", "list", "watch", "create", "delete", "update"]
  - apiGroups: [""]
    resources: ["persistentvolumeclaims", "nodes"]
    verbs: ["get", "list", "watch", "update"]
  - apiGroups: [""]
    resources: ["events"]
    verbs: ["get", "list", "watch", "create", "update", "patch"]
  - apiGroups: [""]
    resources: ["secrets", "namespaces"]
    verbs: ["get", "list"]
  - apiGroups: [""]
    resources: ["nodes", "pods"]
    verbs: ["get", "list", "watch", "update"]
  - apiGroups: ["storage.k8s.io"]
    resources: ["volumeattachments", "volumeattachments"]
    verbs: ["get", "list", "watch", "update", "patch"]
  - apiGroups: ["storage.k8s.io"]
    resources: ["storageclasses"]
    verbs: ["get", "list", "watch"]
---
kind: ClusterRoleBinding
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  name: cfsturbo-csi-node-rolebinding
subjects:
  - kind: ServiceAccount
    name: cfsturbo-csi-node-sa
    namespace: kube-system
roleRef:
  kind: ClusterRole
  name: cfsturbo-csi-node-role
  apiGroup: rbac.authorization.k8s.io
```

### Deploying a Node Plugin

1. Run the `kubectl apply -f csidriver.yaml` command. The following csidriver.yaml code is for your reference:
```yaml
apiVersion: storage.k8s.io/v1beta1
kind: CSIDriver
metadata:
  name: com.tencent.cloud.csi.cfsturbo
spec:
  attachRequired: false
  podInfoOnMount: false
```

2. Run the `kubectl apply -f csi-node.yaml` commad. The following csi-node.yaml code is for your reference:
```yaml
# This YAML file contains driver-registrar & csi driver nodeplugin API objects
# that are necessary to run CSI nodeplugin for cfsturbo
kind: DaemonSet
apiVersion: apps/v1
metadata:
  name: cfsturbo-csi-node
  namespace: kube-system
spec:
  selector:
    matchLabels:
      app: cfsturbo-csi-node
  template:
    metadata:
      labels:
        app: cfsturbo-csi-node
    spec:
      serviceAccount: cfsturbo-csi-node-sa
      hostNetwork: true
      containers:
        - name: driver-registrar
          image: ccr.ccs.tencentyun.com/tkeimages/csi-node-driver-registrar:v1.2.0
          lifecycle:
            preStop:
              exec:
                command: ["/bin/sh", "-c", "rm -rf /registration/com.tencent.cloud.csi.cfsturbo /registration/com.tencent.cloud.csi.cfsturbo-reg.sock"]
          args:
            - "--v=5"
            - "--csi-address=/plugin/csi.sock"
            - "--kubelet-registration-path=/var/lib/kubelet/plugins/com.tencent.cloud.csi.cfsturbo/csi.sock"
          env:
            - name: KUBE_NODE_NAME
              valueFrom:
                fieldRef:
                  fieldPath: spec.nodeName
          volumeMounts:
            - name: plugin-dir
              mountPath: /plugin
            - name: registration-dir
              mountPath: /registration
        - name: cfsturbo
          securityContext:
            privileged: true
            capabilities:
              add: ["SYS_ADMIN"]
            allowPrivilegeEscalation: true
          image: ccr.ccs.tencentyun.com/tkeimages/csi-tencentcloud-cfsturbo:v1.2.2
          args :
            - "--nodeID=$(NODE_ID)"
            - "--endpoint=$(CSI_ENDPOINT)"
          env:
            - name: NODE_ID
              valueFrom:
                fieldRef:
                  fieldPath: spec.nodeName
            - name: CSI_ENDPOINT
              value: unix://plugin/csi.sock
          imagePullPolicy: "IfNotPresent"
          volumeMounts:
            - name: plugin-dir
              mountPath: /plugin
            - name: pods-mount-dir
              mountPath: /var/lib/kubelet/pods
              mountPropagation: "Bidirectional"
            - name: global-mount-dir
              mountPath: /etc/cfsturbo/global
              mountPropagation: "Bidirectional"
      volumes:
        - name: plugin-dir
          hostPath:
            path: /var/lib/kubelet/plugins/com.tencent.cloud.csi.cfsturbo
            type: DirectoryOrCreate
        - name: pods-mount-dir
          hostPath:
            path: /var/lib/kubelet/pods
            type: Directory
        - name: registration-dir
          hostPath:
            path: /var/lib/kubelet/plugins_registry
            type: Directory
        - name: global-mount-dir
          hostPath:
            path: /etc/cfsturbo/global
            type: DirectoryOrCreate
```


### Using a CFS Turbo volume

1. Create a CFS Turbo file system. For more information, see [Creating a File System](#create-cfs).  
2. Use the following template to create a PV of CFS Turbo type.  
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
	  # volumeHandle in PV must be unique, use pv name is better
    volumeHandle: pv-cfsturbo
    volumeAttributes: 
      # cfs turbo server ip
      host: 10.0.0.116
      # cfs turbo fsid (not cfs id)
      fsid: xxxxxxxx
      # cfs turbo rootdir
      rootdir: /cfs
      # cfs turbo subPath
      path: /
      proto: lustre
  storageClassName: ""
```
Parameter description:  
  - **metadata.name**: The name of the created PV.  
  - **spec.csi.volumeHandle**: It must be consistent with the PV name.   
  - **spec.csi.volumeAttributes.host**: The IP address of the file system. You can check it in the information about file system mount target.   
  - **spec.csi.volumeAttributes.fsid**: The fsid of the file system (not the file system ID). You can check it in the file system mount target information. It is the string after "tcp0:/" and before "/cfs" in the mounting command, as shown in the following figure.
  - **spec.csi.volumeAttributes.rootdir**: The root directory of the file system. “/cfs” is entered if it is left empty (the general mounting performance is enhanced if mounting to “/cfs”). If you want to specify a root directory for mounting, you must ensure that the root directory exists in the file system.
  - **spec.csi.volumeAttributes.path**: The subdirectory of the file system. “/” is entered if it is left empty. If you want to specify a subdirectory for mounting, you must ensure that the subdirectory exists in rootdir of the file system. The directory accessed by the container is the rootdir+path directory of the file system (defaults to “/cfs/” directory).
  - **spec.csi.volumeAttributes.proto**: The default protocol for mounting the file system.  
![](https://qcloudimg.tencent-cloud.cn/raw/3ad882f79487144c636ade809b145c1f.png)
>! You need to install a Client in the cluster node according to the version of operating system kernel before using `lustre` protocol to mount a CFS Turbo volume. For details, see [Using CFS Turbo on Linux Clients](https://intl.cloud.tencent.com/document/product/582/40298).


3. Use the following template to create a PVC that binds a PV.  
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
  - **spec.volumeName**: This need to be consistent with the name of PV created in the previous step.  


4. Use the following template to create a Pod that mounts a PVC.  
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
