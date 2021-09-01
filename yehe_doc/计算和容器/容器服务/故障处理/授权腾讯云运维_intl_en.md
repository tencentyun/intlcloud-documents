Tencent Cloud OPS team is not allowed to log in to your cluster for troubleshooting without your permission. If you need Tencent Cloud OPS team to assist in troubleshooting, please refer to the following steps to grant Tencent Cloud OPS team related permissions. You can cancel the permissions at any time.





## Grant permissions to Tencent Cloud though console

1. Log in to the Tencent Cloud TKE console

2. Open the details page of the target cluster

3. Enter the permission management page

   ![](https://main.qcloudimg.com/raw/b17eb7c373aaba218568f715e4e4e02e.png)

4. Click **Authorize Tencent Cloud OPS team**

5. Select the permissions to be granted to Tencent Cloud OPS team

   ![](https://main.qcloudimg.com/raw/75f16899f2c7e2a44656958e4fa8c740.png)

6. Wait for the ticket reply or response from customer service

7. Cancel the permissions

>! Tencent Cloud OPS team is only allowed to log in to the cluster authorized by you. You can withdraw permissions authorized to Tencent Cloud OPS team at any time by deleting relevant resources (ClusterRoleBinding/tkeopsaccount-ClusterRole, ServiceAccount/tkeopsaccount,  and Sercet/tkeopsaccount-token-xxxx).



## Grant permissions to Tencent Cloud OPS team through Kubernetes API

You can grant permissions to Tencent Cloud OPS team by creating the following kubernetes resources.

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

1. Names and labels should be created according to above rules
2. roleRef can be replaced with the permissions you want to grant to Tencent Cloud OPS team

#### Optional: ClusterRole/Role: specifies the permission to be granted to Tencent Cloud OPS team. If there is relevant ClusterRole/Role in the cluster, you can use ClusterRoleBinding/RoleBinding to associate.

Policies will be created automatically if you authorize through console.

Admin Permissions:

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

Read-only Permissions:

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

