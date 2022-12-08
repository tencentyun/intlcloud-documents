This document describes how to use qGPU online/offline hybrid deployment.
## Step 1. Deploy add-ons
You need to deploy nano-gpu-scheduler and nano-gpu-agent.
#### Deploying nano-gpu-scheduler
nano-gpu-scheduler involves `ClusterRole` and `ClusterRoleBinding` as well as `Deployment` and `Service`. Deploy it by using the following YAML.
Below is the scheduling policy:
- By default, online Pods are preferentially scheduled to GPU cards without offline Pods according to the spread algorithm.
- By default, offline Pods are preferentially scheduled to GPU cards without online Pods according to the bin packing algorithm.

```
kind: Deployment
apiVersion: apps/v1
metadata:
  name: qgpu-scheduler
  namespace: kube-system
spec:
  replicas: 1
  selector:
    matchLabels:
      app: qgpu-scheduler
  template:
    metadata:
      labels:
        app: qgpu-scheduler
      annotations:
        scheduler.alpha.kubernetes.io/critical-pod: ''
    spec:
      hostNetwork: true
      tolerations:
        - effect: NoSchedule
          operator: Exists
          key: node-role.kubernetes.io/master
      serviceAccount: qgpu-scheduler
      containers:
        - name: qgpu-scheduler
          image: ccr.ccs.tencentyun.com/lionelxchen/mixed-scheduler:v61         
          command: ["qgpu-scheduler", "--priority=binpack"]
          env:
            - name: PORT
              value: "12345"
          resources:
            limits:
              memory: "800Mi"
              cpu: "1"
            requests:
              memory: "800Mi"
              cpu: "1"
---
apiVersion: v1
kind: Service
metadata:
  name: qgpu-scheduler
  namespace: kube-system
  labels:
    app: qgpu-scheduler
spec:
  ports:
    - port: 12345
      name: http
      targetPort: 12345
  selector:
    app: qgpu-scheduler
---
kind: ClusterRole
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  name: qgpu-scheduler
rules:
  - apiGroups:
      - ""
    resources:
      - nodes
    verbs:
      - get
      - list
      - watch
  - apiGroups:
      - ""
    resources:
      - events
    verbs:
      - create
      - patch
  - apiGroups:
      - ""
    resources:
      - pods
    verbs:
      - update
      - patch
      - get
      - list
      - watch
  - apiGroups:
      - ""
    resources:
      - bindings
      - pods/binding
    verbs:
      - create
  - apiGroups:
      - ""
    resources:
      - configmaps
    verbs:
      - get
      - list
      - watch
---
apiVersion: v1
kind: ServiceAccount
metadata:
  name: qgpu-scheduler
  namespace: kube-system
---
kind: ClusterRoleBinding
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  name: qgpu-scheduler
  namespace: kube-system
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: qgpu-scheduler
subjects:
  - kind: ServiceAccount
    name: qgpu-scheduler
    namespace: kube-system`
```

#### Deploying nano-gpu-agent
nano-gpu-agent involves `ClusterRole` and `ClusterRoleBinding` as well as `Deployment` and `Service`. Deploy it by using the following YAML.
```
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: qgpu-manager
  namespace: kube-system
spec:
  selector:
    matchLabels:
      app: qgpu-manager
  template:
    metadata:
      annotations:
        scheduler.alpha.kubernetes.io/critical-pod: ""
      labels:
        app: qgpu-manager
    spec:
      serviceAccount: qgpu-manager
      hostNetwork: true
      nodeSelector:
        qgpu-device-enable: "enable"
      initContainers:
        - name: qgpu-installer
          image: ccr.ccs.tencentyun.com/lionelxchen/mixed-manager:v27
          command: ["/usr/bin/install.sh"]
          securityContext:
            privileged: true
          volumeMounts:
            - name: host-root
              mountPath: /host
      containers:
        - image: ccr.ccs.tencentyun.com/lionelxchen/mixed-manager:v27
          command: ["/usr/bin/qgpu-manager", "--nodename=$(NODE_NAME)", "--dbfile=/host/var/lib/qgpu/meta.db"]
          name: qgpu-manager
          resources:
            limits:
              memory: "300Mi"
              cpu: "1"
            requests:
              memory: "300Mi"
              cpu: "1"
          env:
            - name: KUBECONFIG
              value: /etc/kubernetes/kubelet.conf
            - name: NODE_NAME
              valueFrom:
                fieldRef:
                  fieldPath: spec.nodeName
          securityContext:
            privileged: true
          volumeMounts:
            - name: device-plugin
              mountPath: /var/lib/kubelet/device-plugins
            - name: pod-resources
              mountPath: /var/lib/kubelet/pod-resources
            - name: host-var
              mountPath: /host/var
            - name: host-dev
              mountPath: /host/dev
      volumes:
        - name: device-plugin
          hostPath:
            path: /var/lib/kubelet/device-plugins
        - name: pod-resources
          hostPath:
            path: /var/lib/kubelet/pod-resources
        - name: host-var
          hostPath:
            type: Directory
            path: /var
        - name: host-dev
          hostPath:
            type: Directory
            path: /dev
        - name: host-root
          hostPath:
            type: Directory
            path: /
---
kind: ClusterRole
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  name: qgpu-manager
rules:
  - apiGroups:
      - ""
    resources:
      - "*"
    verbs:
      - get
      - list
      - watch
  - apiGroups:
      - ""
    resources:
      - events
    verbs:
      - create
      - patch
  - apiGroups:
      - ""
    resources:
      - pods
    verbs:
      - update
      - patch
      - get
      - list
      - watch
  - apiGroups:
      - ""
    resources:
      - nodes/status
    verbs:
      - patch
      - update
---
apiVersion: v1
kind: ServiceAccount
metadata:
  name: qgpu-manager
  namespace: kube-system
---
kind: ClusterRoleBinding
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  name: qgpu-manager
  namespace: kube-system
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: qgpu-manager
subjects:
  - kind: ServiceAccount
    name: qgpu-manager
    namespace: kube-system
```

## Step 2. Configure the node label
All qGPU nodes in the cluster will be labeled "qgpu-device-enable=enable". In addition, you need to add the "mixed-qgpu-enable=enable" label to nodes that require online/offline deployment.

## Step 3. Configure business attributes
<dx-tabs>
::: Offline Pods
You can use `tke.cloud.tencent.com/app-class: offline` to identify an offline Pod and use `tke.cloud.tencent.com/qgpu-core-greedy` to apply for computing power for it. Note that an offline Pod doesn't support multiple cards, and the computing power applied for must be no more than 100 cores.
```yaml
apiVersion: v1
kind: Pod
annotations:
 tke.cloud.tencent.com/app-class: offline
 spec:
  containers:
  - name: offline-container
    resources:
      requests:
	   tke.cloud.tencent.com/qgpu-core-greedy: xx // Offline computing power
       tke.cloud.tencent.com/qgpu-memory: xx
```
:::
::: Online Pods
You can use `tke.cloud.tencent.com/app-class: online` to identify an online Pod. You need to apply for only video memory but not computing power.
```yaml
apiVersion: v1
kind: Pod
annotations:
 tke.cloud.tencent.com/app-class: online
 spec:
  containers:
  - name: online-container
    resources:
      requests:
	     tke.cloud.tencent.com/qgpu-memory: xx
```
:::
::: General Pods
The `tke.cloud.tencent.com/app-class` annotation is not involved. A general Pod supports multiple cards.
```yaml
apiVersion: v1
kind: Pod
spec:
  containers:
  - name: common-container
    resources:
      requests:
       tke.cloud.tencent.com/qgpu-core: xx    
       tke.cloud.tencent.com/qgpu-memory: xx                                       
```              

:::
</dx-tabs>

 
