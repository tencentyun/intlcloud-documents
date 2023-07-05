

## Overview
You can mount a CFS Turbo storage for a cluster by installing a `kubernetes-csi-tencentloud` add-on. This add-on is used to mount the Tencent Cloud CFS Turbo file system to a workload based on a private protocol. Currently, only static configuration is supported.

For more information about CFS storage types, see [Storage Types and Performance Specification](https://intl.cloud.tencent.com/document/product/582/33745).

## Prerequisites
- You have created a TKE cluster or created a Kubernetes cluster on Tencent Cloud, and the cluster version is 1.14 or above.
- kube-apiserver and kubelet have enabled the privilege level, i.e. `--allow-privileged = true`.
- The add-on `feature gates` has been set to `CSINodeInfo = true, CSIDriverRegistry = true`.

## Directions
### Deploying a RBAC policy
If you want to mount a CFS Turbo volume, you need to run the `kubectl apply -f  csi-node-rbac.yaml` command to deploy a RBAC policy in the cluster. The following csi-node-rbac.yaml code is for your reference:
```
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
```
apiVersion: storage.k8s.io/v1beta1
kind: CSIDriver
metadata:
  name: com.tencent.cloud.csi.cfsturbo
spec:
  attachRequired: false
  podInfoOnMount: false
```

2. Run the `kubectl apply -f csi-node.yaml` commad. The following csi-node.yaml code is for your reference:
```
# This YAML file contains driver-registrar & csi driver nodeplugin API objects
# that are necessary to run CSI nodeplugin for cfs
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
          image: ccr.ccs.tencentyun.com/k8scsi/csi-node-driver-registrar:v1.2.0
          lifecycle:
            preStop:
              exec:
                command: ["/bin/sh", "-c", "rm -rf /registration/com.tencent.cloud.csi.cfsturbo/registration/com.tencent.cloud.csi.cfsturbo-reg.sock"]
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
          image: ccr.ccs.tencentyun.com/k8scsi/csi-tencentcloud-cfsturbo:v1.2.0
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
```

### Using a CFS Turbo volume
1. Create a CFS Turbo file system. For details, see [Creating a File System and Mount Point](https://intl.cloud.tencent.com/document/product/582/9132).
2. Use the following template to create a PV of CFS Turbo type.
```
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
      proto: lustre
  storageClassName: ""
```
>! You need to install a Client in the cluster node according to the version of operating system kernel before using `lustre` protocol to mount a CFS Turbo volume. For details, see [Using CFS Turbo on Linux Clients](https://intl.cloud.tencent.com/zh/document/product/582/40298).

3. Use the following template to create a PVC that binds a PV.
```
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

4. Use the following template to create a Pod that mounts a PVC.
```
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
>! Turbo storage created in the CFS console only supports mounting through private protocol. For information on mounting through NFS protocol, see [Using CFS Turbo to Integrate with TKE](https://intl.cloud.tencent.com/zh/document/product/582/42255).
