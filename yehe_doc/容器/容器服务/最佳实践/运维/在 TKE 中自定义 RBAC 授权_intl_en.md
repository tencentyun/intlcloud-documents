

TKE allows you to manage the general authorization of sub-accounts by using the **authorization management** feature in the console and customize your authorization by using a custom YAML ([Using RBAC Authorization](https://kubernetes.io/zh/docs/reference/access-authn-authz/rbac/)). Kubernetes RBAC authorization description and principle are as shown below:

- **Permission objects (Role or ClusterRole)**: Use apiGroups, resources, and verbs to define permissions, including:
	- Role permission object: Used for a specific namespace.  
	- ClusterRole permission object: It can be reused for authorization in multiple namespaces (RoleBinding) or the entire cluster (ClusterRoleBinding).  
- **Authorization object (Subjects)**: The subjects for granting permissions, including three types of subjects: User, Group, and ServiceAccount.  
- **Permission binding (RoleBinding or ClusterRoleBinding)**: It combines and binds the permission objects and authorization objects, including:
	- RoleBinding: Used for a specific namespace.  
	- ClusterRoleBinding: Used for the entire cluster.  

Kubernetes RBAC authorization mainly provides the following four permission binding methods. This document describes how to use them for user authorization management.  


| Method | Description | 
|---------|---------|
| [Method 1. Bind permissions in a namespace](#way1) |  RoleBinding references a Role object to grant Subjects resource permissions in a namespace.  |
|[Method 2. Reuse permission objects for binding in multiple namespaces](#way2) | Different RoleBinding objects in multiple namespaces can reference the same ClusterRole object template to grant Subjects the same template permissions.  | 
|[Method 3. Bind permissions in the entire cluster](#way3) | ClusterRoleBinding references the ClusterRole template to grant Subjects permissions for the entire cluster.  | 
|[Method 4. Customize permissions](#way4)|You can customize permissions, for example, grant a user the permission to log in to the TKE cluster in addition to the preset read-only permission.|


>?In addition to the above methods, you can combine ClusterRole with other ClusterRoles by using aggregationRule on Kubernetes RBAC v1.9 or later. For more information, see [Aggregated ClusterRoles](https://kubernetes.io/zh/docs/reference/access-authn-authz/rbac/#aggregated-clusterroles).  








## Method 1. Bind permissions in a namespace[](id:way1)

This method is mainly used to bind related permissions under a certain namespace for a certain user. It is suitable for scenarios that require refined permissions. For example, developers, testers, and Ops personnel can only manipulate resources in their respective namespaces. The following describes how to implement permission binding for a namespace in TKE.  

1. Use the following shell script to create a test namespace and a test user of ServiceAccount type, and set up cluster access credential (token) authentication as shown below:
```bash
USERNAME='sa-acc' # Set the test account name
NAMESPACE='sa-test' # Set the test namespace name
CLUSTER_NAME='cluster_name_xxx' # Set the test cluster name
# Create the test namespace
kubectl  create namespace ${NAMESPACE} 
# Create the test ServiceAccount account
kubectl create sa ${USERNAME} -n ${NAMESPACE} 
# Obtain the Secret token resource name automatically created by the ServiceAccount account
SECRET_TOKEN=$(kubectl get sa ${USERNAME} -n ${NAMESPACE} -o jsonpath='{.secrets[0].name}')
# Get the plaintext token of the Secrets
SA_TOKEN=$(kubectl get secret ${SECRET_TOKEN} -o jsonpath={.data.token} -n sa-test | base64 -d)
# Set an access credential of token type using the obtained plaintext token information
kubectl config set-credentials ${USERNAME} --token=${SA_TOKEN}
# Set the context entries for accessing the cluster
kubectl config set-context ${USERNAME} --cluster=${CLUSTER_NAME} --namespace=${NAMESPACE} --user=${USERNAME}
```
2. Run the `kubectl config get-contexts` command to view the generated contexts as shown below: 
![image-20201020105559159](https://main.qcloudimg.com/raw/40f7223c29d2c78b5e1671afe28933ba.png)
3. Create a Role permission object resource file `sa-role.yaml` as shown below:
<dx-codeblock>
:::  yaml
kind: Role
apiVersion: rbac.authorization.k8s.io/v1
metadata: 
    namespace: sa-test # Specify the namespace
    name: sa-role-test
rules: # Set the permission rule
- apiGroups: ["", "extensions", "apps"]
  resources: ["deployments", "replicasets", "pods"]
  verbs: ["get", "list", "watch", "create", "update", "patch", "delete"]
  :::
  </dx-codeblock>
4. Create a RoleBinding object resource file `sa-rb-test.yaml`. The following permission binding indicates that the `sa-acc` user of ServiceAccount type has `sa-role-test` (Role type) permissions in the `sa-test` namespace, as shown below:
<dx-codeblock>
:::  yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata: 
    name: sa-rb-test
    namespace: sa-test 
subjects: 
- kind: ServiceAccount
  name: sa-acc
  namespace: sa-test # The namespace of the ServiceAccount 
  apiGroup: ""  # The default apiGroup is `rbac.authorization.k8s.io`.
  roleRef: 
  kind: Role
  name: sa-role-test
  apiGroup: ""  # The default apiGroup is `rbac.authorization.k8s.io`.
  :::
  </dx-codeblock>
5. From the verification result as shown below, you can find that when the Context is `sa-context`, the default namespace is `sa-test`, and it has the permissions configured in the `sa-role-test` (Role) object under the `sa-test` namespace, but it has no permissions under the `default` namespace.  
![image-20201020111456470](https://main.qcloudimg.com/raw/237a717756c26ed8ed654851c2d7aa01.png)




## Method 2. Reuse permission objects for binding in multiple namespaces[](id:way2)

This method is mainly used to grant the same permissions in multiple namespaces to a user. It is suitable for scenarios where a permission template is used to bind permissions in multiple namespaces. For example, you might want to bind the same resource operation permissions for DevOps personnel in multiple namespaces. The following describes how to reuse cluster permissions in multiple namespaces in TKE.  

1. Use the following shell script to create an user authenticated with X.509 self-signed certificate, approve the CSR and the certificate as trustworthy, and set the cluster resource access credential Context as shown below:
```bash
USERNAME='role_user' # Set the username
NAMESPACE='default' # Set the test namespace name
CLUSTER_NAME='cluster_name_xxx' # Set the test cluster name
# Use OpenSSL to generate a self-signed certificate key
openssl genrsa -out ${USERNAME}.key 2048
# Use OpenSSL to generate a self-signed CSR file, where `CN` indicates the username and `O` indicates the group name
openssl req -new -key ${USERNAME}.key -out ${USERNAME}.csr -subj "/CN=${USERNAME}/O=${USERNAME}" 
# Create a Kubernetes CSR
cat <<EOF | kubectl apply -f -
apiVersion: certificates.k8s.io/v1beta1
kind: CertificateSigningRequest
metadata:
      name: ${USERNAME}
spec:
      request: $(cat ${USERNAME}.csr | base64 | tr -d '\n')
      usages:
      - digital signature
      - key encipherment
      - client auth
EOF
# Approve the certificate as trustworthy
kubectl certificate approve ${USERNAME}
# Obtain the self-signed certificate CRT
kubectl get csr ${USERNAME} -o jsonpath={.status.certificate} | base64 --decode > ${USERNAME}.crt
# Set the cluster resource access credential (X.509 certificate)
kubectl config set-credentials ${USERNAME} --client-certificate=${USERNAME}.crt --client-key=${USERNAME}.key
# Set the Context cluster and default namespace
kubectl config set-context  ${USERNAME} --cluster=${CLUSTER_NAME} --namespace=${NAMESPACE} --user=${USERNAME}
```
2. Create a ClusterRole object resource file `test-clusterrole.yaml` as shown below:
<dx-codeblock>
:::  yaml
kind: ClusterRole
apiVersion: rbac.authorization.k8s.io/v1
metadata: 
    name: test-clusterrole
rules: 
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["get", "watch", "list", "create"]
  :::
  </dx-codeblock>
3. Create a RoleBinding object resource file `clusterrole-rb-test.yaml`. The following permission binding indicates that the `role_user` user with the self-signed certificate authentication has `test-clusterrole` (ClusterRole type) permissions in the `default` namespace, as shown below:
<dx-codeblock>
:::  yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata: 
    name: clusterrole-rb-test
    namespace: default 
subjects: 
- kind: User
  name: role_user
  namespace: default # The namespace of the user 
  apiGroup: ""  # The default apiGroup is `rbac.authorization.k8s.io`.
  roleRef: 
  kind: ClusterRole
  name: test-clusterrole
  apiGroup: ""  # The default apiGroup is `rbac.authorization.k8s.io`.
  :::
  </dx-codeblock>
4. From the verification result as shown below, you can find that when the Context is `role_user`, the default namespace is `default`, and it has the permissions configured by the `test-clusterrole` permission object.  
![image-20201020114653469](https://main.qcloudimg.com/raw/2d57f7719b3f8d1b187b41943e396bd5.png)
5. Create the second RoleBinding object resource file `clusterrole-rb-test2.yaml`. The following permission binding indicates that the `role_user` user with the self-signed certificate authentication has `test-clusterrole` (ClusterRole type) permissions in the `default2` namespace.  
<dx-codeblock>
:::  yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata: 
    name: clusterrole-rb-test
    namespace: default2 
subjects: 
- kind: User
  name: role_user
  namespace: default # The namespace of the user 
  apiGroup: ""  # The default apiGroup is `rbac.authorization.k8s.io`.
  roleRef: 
  kind: ClusterRole
  name: test-clusterrole
  apiGroup: ""  # The default apiGroup is `rbac.authorization.k8s.io`.
  :::
  </dx-codeblock>
6. From the verification result as shown below, you can find that in the `default2` namespace, `role_user` also has the permissions configured by `test-clusterrole`. At this point, you have implemented permission reuse and binding in multiple namespaces.  
![image-20201020114512915](https://main.qcloudimg.com/raw/b948a35d0e49f1f99084b2cf8e6b7eb9.png)



## Method 3. Bind permissions in the entire cluster[](id:way3)

This method is mainly used to bind permissions of all namespaces for a user. It is suitable for cluster-wide authorization, such as log collection permission and admin permission. The following directions describe how to use multiple namespaces in TKE to reuse cluster permission for authorization binding.  

1. Create a ClusterRoleBinding object resource file `clusterrole-crb-test3.yaml`. The following permission binding indicates that the `role_user` user with the certificate authentication has `test-clusterrole` (ClusterRole type) permissions in the entire cluster.  
<dx-codeblock>
:::  yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata: 
    name: clusterrole-crb-test
subjects: 
- kind: User
  name: role_user
  namespace: default # The namespace of the user 
  apiGroup: ""  # The default apiGroup is `rbac.authorization.k8s.io`.
  roleRef: 
  kind: ClusterRole
  name: test-clusterrole
  apiGroup: ""  # The default apiGroup is `rbac.authorization.k8s.io`.
  :::
  </dx-codeblock>
2. From the verification result as shown below, you can find that after the YAML of permission binding is applied, `role_user` has the cluster-wide `test-clusterrole` permissions.  
![image-20201020141737129](https://main.qcloudimg.com/raw/5f3415f45bac5b622264fd4929e104a5.png)

## Method 4. Customize permissions[](id:way4)
This section describes how to grant a user custom permissions as a cluster admin, including preset read-only permission and additional permission to log in to the TKE cluster.

#### 1. Authorize
First, grant read-only permission to a specified user as instructed in [Using Preset Identity Authorization](https://intl.cloud.tencent.com/document/product/457/37368).

#### 2. View user information in the RBAC
View the information of the user bound to the read-only ClusterRoleBinding, which is to be bounded to the new ClusterRoleBinding. As shown below, you need to view the details in the ClusterRoleBinding object of the specified user.
![](https://qcloudimg.tencent-cloud.cn/raw/cc373e0fe3343fdf18638211b13190fe.png)

```yaml
subjects:
- apiGroup: rbac.authorization.k8s.io
  kind: User
  name: 700000xxxxxx-1650879262  # The username of the specified user in RBAC. You need to get this information of the specified user.
```

#### 3. Create a ClusterRole
Create a ClusterRole through YAML for a read-only user with TKE login permission as shown below:

```yaml
apiVersion: rbac.authorization.k8s.io/v1beta1
kind: ClusterRole
metadata:
  name: "700000xxxxxx-ClusterRole-ro"  # ClusterRole name
rules:
- apiGroups:
  - ""
  resources:
  - pods
  - pods/attach
  - pods/exec  # Pod login permission
  - pods/portforward
  - pods/proxy
  verbs:
  - create
  - get
  - list
  - watch
```

#### 4. Create a ClusterRoleBinding
Create the YAML file of the ClusterRoleBinding for the specified user as shown below:

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: "700000xxxxxx-ClusterRoleBinding-ro"
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: "700000xxxxxx-ClusterRole-ro"  # Use the ClusterRole name in step 3
subjects:
- apiGroup: rbac.authorization.k8s.io
  kind: User
  name: "700000xxxxxx-1650879262"  # Use the user information in step 2
```

## Summary

Combined with Tencent Cloud access permission management and Kubernetes RBAC authorization mode, the authorization management feature in the TKE console becomes simple and convenient, which can meet the permission management scenarios of most Tencent Cloud sub-accounts. The custom permission binding through YAML is more flexible and suitable for complex and personalized user permission control. You can choose a permission management method as needed.  

