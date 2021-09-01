默认情况下腾讯云无法登录集群进行问题排障，如果您需要腾讯云售后协助进行运维排障，请参考以下步骤授予腾讯云运维权限。您有权随时吊销回收授予腾讯云的运维排障权限。 





## 通过控制台授权腾讯云权限

1. 登陆腾讯云容器服务控制台

2. 进入需要腾讯云协助的集群详情

3. 进入权限管理页面

   ![](https://main.qcloudimg.com/raw/b17eb7c373aaba218568f715e4e4e02e.png)

4. 点击授权腾讯云运维

5. 选择赋予腾讯云的操作权限

   ![](https://main.qcloudimg.com/raw/75f16899f2c7e2a44656958e4fa8c740.png)

6. 等待工单/售后反馈意见

7. 删除权限

>! 腾讯云仅能够登陆您授权的集群，您可以随时吊销腾讯云运维权限， 您可以通过删除相关资源（ClusterRoleBinding/tkeopsaccount-ClusterRole、ServiceAccount/tkeopsaccount、Sercet/tkeopsaccount-token-xxxx）吊销腾讯云运维权限。



## 通过Kubernetes API授予腾讯云权限

您可以通过创建以下kubernetes资源授予腾讯云制定权限

#### ServiceAccount： 授予腾讯云访问集群凭证

```yaml
kind: ServiceAccount
apiVersion: v1
metadata:
  name: tkeopsaccount
  namespace: kube-system
  labels:
    cloud.tencent.com/tke-ops-account: tkeops
```



#### ClusterRoleBinding/RoleBing：授予腾讯云的操作权限规则

```yaml
apiVersion: rbac.authorization.k8s.io/v1beta1
kind: ClusterRoleBinding
metadata:
  annotations:
    cloud.tencent.com/tke-ops-account: tkeops
  labels:
    cloud.tencent.com/tke-ops-account: tkeops
  name: tkeopsaccount-ClusterRole
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: tke:admin
subjects:
- kind: ServiceAccount
  name: tkeopsaccount
  namespace: kube-system
```

1. 名称和label需按上述规则创建
2. roleRef可替换为您期望授权腾讯云的权限

#### 可选：ClusterRole/Role:授予腾讯云的操作权限， 如集群内有相关ClusterRole/Role可直接使用ClusterRoleBinding/RoleBinding关联

通过控制台授权，将自动创建策略，无需单独创建。

管理员权限：

```yaml
apiVersion: rbac.authorization.k8s.io/v1beta1
kind: ClusterRole
metadata:
  labels:
    cloud.tencent.com/tke-rbac-generated: "true"
  name: tke:admin
rules:
- apiGroups:
  - '*'
  resources:
  - '*'
  verbs:
  - '*'
- nonResourceURLs:
  - '*'
  verbs:
  - '*'

```

只读权限：

```yaml
apiVersion: rbac.authorization.k8s.io/v1beta1
kind: ClusterRole
metadata:
  labels:
    cloud.tencent.com/tke-rbac-generated: "true"
  name: tke:ro
rules:
- apiGroups:
  - ""
  resources:
  - pods
  - pods/attach
  - pods/exec
  - pods/portforward
  - pods/proxy
  verbs:
  - get
  - list
  - watch
- apiGroups:
  - ""
  resources:
  - configmaps
  - endpoints
  - persistentvolumeclaims
  - replicationcontrollers
  - replicationcontrollers/scale
  - secrets
  - serviceaccounts
  - services
  - services/proxy
  verbs:
  - get
  - list
  - watch
- apiGroups:
  - ""
  resources:
  - nodes
  - persistentvolumes
  verbs:
  - get
  - list
  - watch
- apiGroups:
  - ""
  resources:
  - events
  - replicationcontrollers/status
  - pods/log
  - pods/status
  - componentstatuses
  verbs:
  - get
  - list
  - watch
- apiGroups:
  - apps
  resources:
  - daemonsets
  - deployments
  - deployments/rollback
  - deployments/scale
  - replicasets
  - replicasets/scale
  - statefulsets
  verbs:
  - get
  - list
  - watch
- apiGroups:
  - autoscaling
  resources:
  - horizontalpodautoscalers
  verbs:
  - get
  - list
  - watch
- apiGroups:
  - storage.k8s.io
  resources:
  - storageclasses
  verbs:
  - get
  - list
  - watch
- apiGroups:
  - batch
  resources:
  - cronjobs
  - jobs
  verbs:
  - get
  - list
  - watch
- apiGroups:
  - extensions
  - networking.k8s.io
  resources:
  - daemonsets
  - deployments
  - deployments/rollback
  - deployments/scale
  - ingresses
  - replicasets
  - replicasets/scale
  - replicationcontrollers/scale
  verbs:
  - get
  - list
  - watch
- apiGroups:
  - servicecatalog.k8s.io
  resources:
  - clusterserviceclasses
  - clusterserviceplans
  - clusterservicebrokers
  - serviceinstances
  - servicebindings
  verbs:
  - get
  - list
  - watch
- apiGroups:
  - policy
  resources:
  - poddisruptionbudgets
  verbs:
  - get
  - list
- apiGroups:
  - networking.istio.io
  - config.istio.io
  - rbac.istio.io
  - authentication.istio.io
  - security.istio.io
  - install.istio.io
  resources:
  - '*'
  verbs:
  - get
  - list
  - watch
- apiGroups:
  - apiextensions.k8s.io
  resources:
  - customresourcedefinitions
  verbs:
  - get
  - list
  - watch
- apiGroups:
  - networking.tke.cloud.tencent.com
  resources:
  - '*'
  verbs:
  - get
  - list
  - watch
- apiGroups:
  - cloud.tencent.com
  resources:
  - '*'
  verbs:
  - get
  - list
  - watch
- apiGroups:
  - ccs.cloud.tencent.com
  resources:
  - '*'
  verbs:
  - get
  - list
  - watch
- apiGroups:
  - cls.cloud.tencent.com
  resources:
  - '*'
  verbs:
  - get
  - list
  - watch

```

