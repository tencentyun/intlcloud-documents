Tencent Cloud OPS team is not allowed to log in to your cluster for troubleshooting without your permission. If you need Tencent Cloud OPS team to assist in troubleshooting, please refer to the following steps to grant Tencent Cloud OPS team related permissions. You can cancel the permissions authorized to Tencent Cloud OPS team at any time.  





## Grant permissions to Tencent Cloud though console
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2/overview).
2. On **Cluster Management** page, select the cluster where Tencent Cloud assistance is needed.
3. On the cluster details page, select **Authorization Management** > **Authorize Tencent Cloud OPS team**, as shown below:
![](https://main.qcloudimg.com/raw/b17eb7c373aaba218568f715e4e4e02e.png)
4. On the **Manage Permissions** page, select the operation permissions that you want to authorize to Tencent Cloud OPS team, as shown below:
![](https://main.qcloudimg.com/raw/75f16899f2c7e2a44656958e4fa8c740.png)
5. Click **Done**. You can check the progress in [My Tickets](https://console.cloud.tencent.com/workorder).
>! Tencent Cloud can only log in to the cluster authorized by you. You can withdraw permissions authorized to Tencent Cloud OPS team at any time by deleting relevant resources (ClusterRoleBinding/tkeopsaccount-ClusterRole, ServiceAccount/tkeopsaccount, and Sercet/tkeopsaccount-token-xxxx).
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
1. Name and label should be created according to the following rule.
2. roleRef can be replaced with the permissions you want to grant to Tencent Cloud OPS team.
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
<dx-codeblock>
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
</dx-codeblock>

