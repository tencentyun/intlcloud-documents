## Overview

TKE supports managing sub-accounts authorization through the **Authorization Management** feature in the console, or customizing YAML <a href="https://kubernetes.io/docs/reference/access-authn-authz/rbac/">(RBAC Authorization)</a> to meet more personalized authorization requirements. The Kubernetes RBAC authorization instructions and principles are as follows:

- **Permission objects (Role or ClusterRole)**: uses apiGroups, resources, and verbs to define permissions, including:
	- Role permission object: a Role always sets permissions within a particular namespace.
	- ClusterRole permission object: a ClusterRole can be reused for multiple namespace authorizations (Rolebinding) or for the entire cluster authorization (ClusterRoleBinding).
- **Authorization object (Subjects)**: the subjects for granting permissions, including three types of subjects: User, Group, and ServiceAccount.
- **Permission Binding (Rolebinding or ClusterRoleBinding)**: combines and binds the permission objects and authorization objects, including:
	- Rolebinding: permission binding for a specific namespace.
	- ClusterRoleBinding: permission binding for the entire cluster.

![RBAC](https://main.qcloudimg.com/raw/4dc8215877eaf990d3f4e5142cfaacdc.png)


As shown in the figure above, Kubernetes RBAC authorization mainly provides the following three permission binding methods. This document describes how to use these three permission binding methods to achieve user authorization management.


| Method | Description |
|---------|---------|
| [Permission binding for a single namespace](#way1) | RoleBinding references a Role object and grants Subjects the resource permission of a certain namespace. |
|[Permission binding for multiple namespaces by reusing the cluster permission object](#way2) | Different RoleBinding in multiple namesspaces can reference the same ClusterRole object template to grant Subjects the same permissions as the template. |
|[Permission binding for the entire cluster](#way3) | The ClusterRolleBinding references the ClusterRole template to grant Subjects the entire cluster permissions. |


>?Starting from Kubernetes RBAC v1.9, you can also create ClusterRole by using aggregationRule to combine with other ClusterRoles. For more information, see [Aggregated ClusterRoles]( https://kubernetes.io/zh/docs/reference/access-authn-authz/rbac/#aggregated-clusterroles).






## Directions

[](id:way1)
### Permission binding for a single namespace

This method is mainly used to bind related permissions of a certain namespace for a certain user, and is suitable for scenarios that require refined permissions. For example, developers, testers, and OPS personnel can only operate on resources in their respective namespaces. The following directions describe how to implement permission binding for a single namespace in TKE.

1. Use the following Shell script to create a test namespace and a test user of ServiceAccount type, and set up cluster access credential (Token) authentication, as shown below:

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
# Obtain the plaintext Token of secrets
SA_TOKEN=$(kubectl get secret ${SECRET_TOKEN} -o jsonpath={.data.token} -n sa-test | base64 -d)
# Set an access credential of token type using the obtained plaintext token information
kubectl config set-credentials ${USERNAME} --token=${SA_TOKEN}
# Set the context entries for accessing the cluster
kubectl config set-context ${USERNAME} --cluster=${CLUSTER_NAME} --namespace=${NAMESPACE} --user=${USERNAME}
```

2. Run the command `kubectl config get-contexts` to view the generated contexts entries, as shown below: 
![image-20201020105559159](https://main.qcloudimg.com/raw/40f7223c29d2c78b5e1671afe28933ba.png)
3. Create a Role permission object resource file “sa-role.yaml”, as shown below:

```yaml
kind: Role
apiVersion: rbac.authorization.k8s.io/v1
metadata: 
    namespace: sa-test # Specify the Namespace
    name: sa-role-test
rules: # Set the permission rule
 - apiGroups: ["", "extensions", "apps"]
  resources: ["deployments", "replicasets", "pods"]
  verbs: ["get", "list", "watch", "create", "update", "patch", "delete"]
```

4. Create a RoleBinding object resource file “sa-rb-test.yaml”. The following permission binding indicates that the sa-acc user of ServiceAccount type has sa-role-test (Role type) permissions in the sa-test namespace, as shown below:

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata: 
    name: sa-rb-test
    namespace: sa-test 
subjects: 
 - kind: ServiceAccount
  name: sa-acc
  namespace: sa-test # The Namespace where ServiceAccount locates 
  apiGroup: ""  # The default apiGroup is rbac.authorization.k8s.io.
roleRef: 
  kind: Role
  name: sa-role-test
  apiGroup: ""  # The default apiGroup is rbac.authorization.k8s.io.
```

5. From the verification result in the following figure, you can find that when the Context is sa-context, the default namespace is sa-test, and it has the permissions configured in the sa-role-test (Role) object under the sa-test namespace, but it has no permission under the default namespace.
![image-20201020111456470](https://main.qcloudimg.com/raw/237a717756c26ed8ed654851c2d7aa01.png)



[](id:way2)
### Permission binding for multiple namespaces by reusing the cluster permission object

This method is mainly used to grant users the same permissions in multiple namespaces. It is suitable for scenarios where a permission template is used to bind authorizations for multiple namespaces. For example, developers need to bind the same resource operations permission in multiple namespaces. The following directions describe how to implement permission binding for multiple namespaces by reusing cluster permission object in TKE.

1. Use the following Shell script to create an user authenticated with X509 self-signed certificate, approve the CSR and the certificate as trustworthy, and set the cluster resource access credential Context, as shown below:

```bash
USERNAME='role_user' # Set the user name that you want to create
NAMESPACE='default' # Set the test namespace name
CLUSTER_NAME='cluster_name_xxx' # Set the test cluster name
# Use Openssl to generate a self-signed certificate key
openssl genrsa -out ${USERNAME}.key 2048
# Use Openssl to generate a self-signed CSR file, with CN indicating the user name and O indicating the group name.
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
# Set the cluster resource access credentials (X509 certificate)
kubectl config set-credentials ${USERNAME} --client-certificate=${USERNAME}.crt --client-key=${USERNAME}.key
# Set Context cluster, default Namespace, etc.
kubectl config set-context  ${USERNAME} --cluster=${CLUSTER_NAME} --namespace=${NAMESPACE} --user=${USERNAME}

```
2. Create a ClusterRole object resource “test-clusterrole.yaml”, as shown below:

``` yaml
kind: ClusterRole
apiVersion: rbac.authorization.k8s.io/v1
metadata: 
    name: test-clusterrole
rules: 
 - apiGroups: [""]
  resources: ["pods"]
  verbs: ["get", "watch", "list", "create"]
```

3. Create a RoleBinding object resource file “clusterrole-rb-test.yaml”. The following permission binding indicates that the user role_user with the self-signed certificate authentication has the test-clusterrole (ClusterRole type) permission in the default namespace, as shown below:

``` yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata: 
    name: clusterrole-rb-test
    namespace: default 
subjects: 
 - kind: User
  name: role_user
  namespace: default # The Namespace where User locates 
  apiGroup: ""  # The default apiGroup is rbac.authorization.k8s.io.
roleRef: 
  kind: ClusterRole
  name: test-clusterrole
  apiGroup: ""  # The default apiGroup is rbac.authorization.k8s.io.
```

4. From the verification result in the figure below, you can find that when the Context is role_user, the default namespace is “default”, and it has the permissions configured by the test-clusterrole permission object.
![image-20201020114653469](https://main.qcloudimg.com/raw/2d57f7719b3f8d1b187b41943e396bd5.png)
5. Create the second RoleBinding object resource file “clusterrole-rb-test2.yaml”. The following permission binding indicates that the user role_user with the self-signed certificate authentication has the test-clusterrole (ClusterRole type) permission in the default2 namespace.

``` yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata: 
    name: clusterrole-rb-test
    namespace: default2 
subjects: 
 - kind: User
  name: role_user
  namespace: default # The Namespace where User locates 
  apiGroup: ""  # The default apiGroup is rbac.authorization.k8s.io.
roleRef: 
  kind: ClusterRole
  name: test-clusterrole
  apiGroup: ""  # The default apiGroup is rbac.authorization.k8s.io.
```

6. From the verification result in the figure below, you can find that in the default2 namespace, role_user also has the permissions configured by test-clusterrole. So far, through the above steps, it has implemented the permission binding for the multiple namespaces by reusing the cluster permissions.
![image-20201020114512915](https://main.qcloudimg.com/raw/b948a35d0e49f1f99084b2cf8e6b7eb9.png)


[](id:way3)
### Permission binding for the entire cluster

This method is mainly used to bind permissions of all namespaces (cluster-scoped) for a user, and is suitable for cluster-scoped authorization scenarios, such as log collection permission, admin permission. The following directions describe how to use multiple namespaces in TKE to reuse cluster permission for authorization binding.

1. Create a ClusterRoleBinding object resource file “clusterrole-crb-test3.yaml”. The following permission binding indicates that the user role_user with the certificate authentication has the test-clusterrole (ClusterRole type) permission in the entire cluster.

``` yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata: 
    name: clusterrole-crb-test
subjects: 
 - kind: User
  name: role_user
  namespace: default # The Namespace where User locates 
  apiGroup: ""  # The default apiGroup is rbac.authorization.k8s.io.
roleRef: 
  kind: ClusterRole
  name: test-clusterrole
  apiGroup: ""  # The default apiGroup is rbac.authorization.k8s.io.
```

2. From the verification result in the figure below, you can find that after the YAML of permission binding is performed, role_user has the cluster-wide test-clusterrole permission.
![image-20201020141737129](https://main.qcloudimg.com/raw/5f3415f45bac5b622264fd4929e104a5.png)



## Summary

Combined with Tencent Cloud access permission management and Kubernetes RBAC authorization mode, the authorization management feature in TKE console becomes simple and convenient, which can meet the permission management scenarios of most Tencent Cloud sub-accounts. The custom permission binding via YAML is more flexible and suitable for complex and personalized user permission management scenarios. Users can choose the permission management method based on the actual authorization requirements.

