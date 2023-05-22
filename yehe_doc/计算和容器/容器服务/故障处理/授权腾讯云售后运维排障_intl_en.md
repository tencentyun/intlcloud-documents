Tencent Cloud OPS team is not allowed to log in to your cluster for troubleshooting without your permission. If you need Tencent Cloud OPS team to assist in troubleshooting, please refer to the following steps to grant Tencent Cloud OPS team related permissions. You can cancel the permissions authorized to Tencent Cloud OPS team at any time.   

## Grant permissions to Tencent Cloud though console
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2/overview).
2. On **Cluster Management** page, select the cluster where Tencent Cloud assistance is needed.
3. On the cluster details page, select **Authorization Management** > **Authorize Tencent Cloud OPS team**.
4. When configuring the cluster RBAC, select the operation permissions that you want to authorize to Tencent Cloud OPS team.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/A56E218_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221226164933.png)
5. After the configuration is completed, you can check the progress in [My Tickets](https://console.cloud.tencent.com/workorder).
>!Tencent Cloud OPS team is not allowed to log in to your cluster for troubleshooting without your permission. If you need Tencent Cloud OPS team to assist in troubleshooting, you can grant Tencent Cloud OPS team related permissions. You can also cancel the permissions authorized to Tencent Cloud OPS team at any time.
You can withdraw permissions authorized to Tencent Cloud OPS team by deleting relevant resources (ClusterRoleBinding/tkeopsaccount-ClusterRole, ServiceAccount/tkeopsaccount, and Sercet/tkeopsaccount-token-xxxx).
>


## Grant permissions to Tencent Cloud OPS team through Kubernetes API

You can grant permissions to Tencent Cloud OPS team by creating the following Kubernetes resources.

#### ServiceAccount: authorize Tencent Cloud OPS team to access cluster credential

```yaml
kind: ServiceAccount
apiVersion: v1
metadata:
  name: tkeopsaccount
  namespace: kube-system
  labels:
    cloud.tencent.com/tke-ops-account: tkeops
```



#### ClusterRoleBinding/RoleBing: rules on granting Tencent Cloud OPS team permissions

>?
>1. Name and label should be created according to the following rule.
>2. roleRef can be replaced with the permissions you want to grant to Tencent Cloud OPS team.
>


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



#### (Optional) ClusterRole/Role: permissions authorized to Tencent Cloud OPS team
If there is relevant ClusterRole/Role in the cluster, you can use ClusterRoleBinding/RoleBinding to associate. Policies will be created automatically if you authorize through console.
<dx-tabs>
::: Admin permissions 
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
:::
::: Read-only
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

:::
</dx-tabs>


