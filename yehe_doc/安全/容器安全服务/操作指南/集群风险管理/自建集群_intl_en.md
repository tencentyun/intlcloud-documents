## Accessing an External Cluster
This document describes how to access an external cluster for unified management and risk check.

### Limits
You can access an external cluster with up to 500 nodes.

### Directions
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Cluster Risk Management** > **Security Check** on the left sidebar.
2. On the **Security Check** page, click **Access external cluster**.
![](https://qcloudimg.tencent-cloud.cn/raw/729901ec2f9a5599a36be41028841405.png)
3. On the **Configure cluster information** page, configure parameters and click **Next**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/9a94b765627b87b386499f4b40deea5c.png" style="zoom:67%;" />

**Parameter description:**
<table>
<thead>
<tr>
<th>Parameter Group</th>
<th>Parameter</th>
<th>Description</th>
<th>Option</th>
</tr>
</thead>
<tbody><tr>
<td rowspan=3>Basic settings</td>
<td>Cluster name</td>
<td>Enter the name of the external cluster, which can contain up to 64 characters.</td>
<td>-</td>
</tr>
<tr>
 <td>Cluster environment</td>
<td>Select the type of the external cluster.</td>
<td>Kubernetes or OpenShift</td>
</tr>
<tr>
 <td>Cluster version</td>
<td>Select the cluster version of the cluster environment.</td>
<td>1.13 or later for Kubernetes clusters</td>
</tr>
<tr>
<td rowspan=4>Networking</td>
<td>Network type</td>
<td>Select the public network or VPC for accessing the external cluster.</td>
<td>Public network or VPC</td>
</tr>
<tr>
 <td>Region</td>
<td>Select the region of the external cluster. There is no limit on the region for the public network.</td>
<td>-</td>
</tr>
<tr>
 <td>VPC ID</td>
<td>Select the VPC information of the cluster when you set the network type to VPC.</td>
<td>-</td>
</tr>
<tr>
 <td>API server address</td>
<td>Select the backend service type of the cluster API server when you set the network type to VPC.</td>
<td>Server or load balancer</td>
</tr>
<tr>
<td rowspan=2>Scanner</td>
<td>Scanner installation</td>
<td>Select the automatic or manual installation of the scanner.</td>
<td><ul><li>Select the automatic installation and perform a security check.</li><li>Select the manual installation and deliver and install the component in the cluster manually after the connection.</li></td>
</tr>
<tr>
 <td>Automatic check</td>
<td>Set whether to enable the automatic check feature of the cluster.</td>
<td><ul><li>Enable</li><li>Disable</li></td>
</tr>
</tbody></table>

4. Click **Select a file**, upload a local configuration file, and click **Complete**.
>!
>- If the self-built cluster is accessed over the public network and the **access control policy** is set, you need to click **Allowed IPs** to add the IP on the page.
>- You need to generate a Kubernetes configuration file on the server before you can upload it. For detailed directions, see [Generating a Kubernetes Configuration File](#K8s).
>- You can upload a configuration file of up to 1 MB.

<img src="https://qcloudimg.tencent-cloud.cn/raw/55cecb9f9157f9ef907a6a23e07175ac.png" style="zoom:67%;" />

## Generating a Kubernetes Configuration File[](id:K8s)
This section describes how to generate a Kubernetes configuration file of the least privilege required by TCSS.

### Prerequisites
- You have set up a Kubernetes cluster on the server as instructed in [Getting started](https://kubernetes.io/docs/setup/).
- You have installed the Docker service.

### Directions
1. Log in to the server of the master node of the Kubernetes cluster as the root user.
2. Enter the following command to create a namespace and bind the permission.
```
# 1. Create the `tcss` namespace
# 2. Create the `tcss-admin` admin role under the `tcss` namespace
# 3. Bind the `tcss-admin` role to the `tcss` user
# 4. Create the `tcss-agent-secret` key and bind it to the `tcss-agent` service account
# 5. Create the `security-clusterrole` read-only cluster role
# 6. Bind the `security-clusterrole` role to the `tcss-agent` service account

---
apiVersion: v1
kind: Namespace
metadata:
  name: tcss


---
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: tcss
  name: tcss-admin
rules:
- apiGroups: ["extensions", "apps", ""]
  resources: ["*"]
  verbs: ["get", "list", "watch", "create", "update", "patch", "delete"]

---
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: tcss-admin-rb
  namespace: tcss
subjects:
- kind: User
  name: tcss
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: Role
  name: tcss-admin
  apiGroup: rbac.authorization.k8s.io


---
apiVersion: v1
kind: Secret
metadata:
  name: tcss-agent-secret
  namespace: tcss
  annotations:
    kubernetes.io/service-account.name: tcss-agent
type: kubernetes.io/service-account-token


---
apiVersion: v1
kind: ServiceAccount
metadata:
  name: tcss-agent
  namespace: tcss
secrets:
  - name: tcss-agent-secret
    namespace: tcss


---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: security-clusterrole
rules:
- apiGroups: ["", "v1"]
  resources: ["namespaces", "pods", "nodes"]
  verbs: ["get", "list"]
- apiGroups: ["apps"]
  resources: ["replicasets", "daemonsets", "deployments", "statefulsets"]
  verbs: ["get", "list"]
- apiGroups: ["batch"]
  resources: ["jobs", "cronjobs"]
  verbs: ["get", "list"]
- apiGroups: ["rbac.authorization.k8s.io"]
  resources: ["clusterroles", "clusterrolebindings"]
  verbs: ["get"]

---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: security-clusterrolebinding
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: security-clusterrole
subjects:
- kind: ServiceAccount
  name: tcss-agent
  namespace: tcss
- kind: User
  name: tcss
  apiGroup: rbac.authorization.k8s.io
```
3. Go to the Kubernetes configuration directory (/etc/kubernetes/) and enter the following command to create a certificate.
```
# Create the `tcss.key` key for `User`
openssl genrsa -out tcss.key 2048

# Create the `tcss.csr` certificate signing request
openssl req -new -key tcss.key -out tcss.csr -subj "/O=K8s/CN=tcss"

# Sign the certificate and generate `tcss.crt`
openssl x509 -req -in tcss.csr -CA ca.crt -CAkey ca.key -CAcreateserial -out tcss.crt -days 365
```
4. Enter the following command to create a cluster configuration file.
```
# Create and set the cluster configuration. Here, the API server address must be a public network address that is accessible.
kubectl config set-cluster tcss --server=https://xx.xx.xx.xx:60002 --certificate-authority=/etc/kubernetes/ca.crt --embed-certs=true --kubeconfig=/root/tcss.conf

# Create and set the user configuration
kubectl config set-credentials tcss --client-certificate=tcss.crt --client-key=tcss.key --embed-certs=true --kubeconfig=/root/tcss.conf

# Set the `context` configuration
kubectl config set-context tcss@tcss --cluster=tcss --user=tcss --kubeconfig=/root/tcss.conf

# Switch the `context` configuration
kubectl config use-context tcss@tcss --kubeconfig=/root/tcss.conf
```
5. Verify and upload the cluster configuration file.
```
KUBECONFIG=/root/tcss.conf kubectl -n tcss get pod
```
>?Run the above command. If the returned result displays a Pod or indicates that there are no relevant resources in the current namespace, the cluster configuration is available, and you just need to upload the file to `/root/tcss.conf`.

### Quick script[](id:yjjb)
On the master node, you can use the following script code to quickly generate a cluster configuration file.
>?You need to install OpenSSL in the environment in advance.
>
```
#!/bin/bash

set -e;

# You need to set `API_SERVER` as the accessible address and port of the public network.
# API_SERVER=https://xx.xx.xx.xx:xxxx

# Set the following paths as needed
KUBECONFIG_TARGET=/root/tcss.conf
CA_FILE=/etc/kubernetes/ca.crt
CAKEY_FILE=/etc/kubernetes/ca.key
TCSS_TMPDIR=/tmp/tcss
# In the OpenShift environment, replace it with `oc`
KUBECTL_CMD=kubectl


if [ ! $API_SERVER ]; then
    echo "API_SERVER does not set.";
    exit 1;
fi
if ! which kubectl ; then
    echo "kubectl does not exist.";
    exit 1;
fi
if [ ! -f "$CA_FILE" ]; then
    echo "$CA_FILE does not exist.";
    exit 1;
fi
if [ ! -f "$CAKEY_FILE" ]; then
    echo "$CAKEY_FILE does not exist.";
    exit 1;
fi
if [ ! -d $TCSS_TMPDIR ]; then
    mkdir -p $TCSS_TMPDIR;
fi

cat <<EOF  > $TCSS_TMPDIR/tcss_res.yaml
---
apiVersion: v1
kind: Namespace
metadata:
  name: tcss

---
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: tcss
  name: tcss-admin
rules:
- apiGroups: ["extensions", "apps", ""]
  resources: ["*"]
  verbs: ["get", "list", "watch", "create", "update", "patch", "delete"]

---
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: tcss-admin-rb
  namespace: tcss
subjects:
- kind: User
  name: tcss
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: Role
  name: tcss-admin
  apiGroup: rbac.authorization.k8s.io

---
apiVersion: v1
kind: Secret
metadata:
  name: tcss-agent-secret
  namespace: tcss
  annotations:
    kubernetes.io/service-account.name: tcss-agent
type: kubernetes.io/service-account-token

---
apiVersion: v1
kind: ServiceAccount
metadata:
  name: tcss-agent
  namespace: tcss
secrets:
  - name: tcss-agent-secret
    namespace: tcss

---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: security-clusterrole
rules:
- apiGroups: ["", "v1"]
  resources: ["namespaces", "pods", "nodes"]
  verbs: ["get", "list"]
- apiGroups: ["apps"]
  resources: ["replicasets", "daemonsets", "deployments", "statefulsets"]
  verbs: ["get", "list"]
- apiGroups: ["batch"]
  resources: ["jobs", "cronjobs"]
  verbs: ["get", "list"]
- apiGroups: ["rbac.authorization.k8s.io"]
  resources: ["clusterroles", "clusterrolebindings"]
  verbs: ["get"]


---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: security-clusterrolebinding
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: security-clusterrole
subjects:
- kind: ServiceAccount
  name: tcss-agent
  namespace: tcss
- kind: User
  name: tcss
  apiGroup: rbac.authorization.k8s.io
EOF

# echo "generate tcss resource file ($TCSS_TMPDIR/tcss_res.yaml) success."

$KUBECTL_CMD apply -f $TCSS_TMPDIR/tcss_res.yaml;

# Create the `tcss.key` key for `User`
openssl genrsa -out $TCSS_TMPDIR/tcss.key 2048
# Create the `tcss.csr` certificate signing request
openssl req -new -key $TCSS_TMPDIR/tcss.key -out $TCSS_TMPDIR/tcss.csr -subj "/O=K8s/CN=tcss"
# Sign the certificate and generate `tcss.crt`
openssl x509 -req -in $TCSS_TMPDIR/tcss.csr -CA $CA_FILE -CAkey $CAKEY_FILE -CAcreateserial -out $TCSS_TMPDIR/tcss.crt -days 365

# Create and set the cluster configuration
$KUBECTL_CMD config set-cluster tcss --server=$API_SERVER --certificate-authority=$CA_FILE --embed-certs=true --kubeconfig=$KUBECONFIG_TARGET
# Create and set the user configuration
$KUBECTL_CMD config set-credentials tcss --client-certificate=$TCSS_TMPDIR/tcss.crt --client-key=$TCSS_TMPDIR/tcss.key --embed-certs=true --kubeconfig=$KUBECONFIG_TARGET
# Set the `context` configuration
$KUBECTL_CMD config set-context tcss@tcss --cluster=tcss --user=tcss --kubeconfig=$KUBECONFIG_TARGET
# Switch the `context` configuration
$KUBECTL_CMD config use-context tcss@tcss --kubeconfig=$KUBECONFIG_TARGET

echo "generate KUBECONFIG file success. $KUBECONFIG_TARGET"
```

## Generating an OpenShift Configuration File
This section describes how to generate an OpenShift configuration file of the least privilege required by TCSS.

### Prerequisites
1. You have set up a Kubernetes cluster on the server as instructed in [Getting started](https://kubernetes.io/docs/setup/).
2. You have installed the Docker service.
3. Currently, only OpenShift 3.0 and later are supported. Earlier versions may involve uncertain issues.

### Directions
>? The overall idea is similar to that described in the previous section. The only difference lies in the path and command line tool. If kubectl has been installed on the master node in the cluster, the directions are the same as those described in the previous section.

1. Log in to the server of the master node in the OpenShift cluster as the root user.
2. Enter the following command to create a namespace and bind the permission.
```
# 1. Create the `tcss` namespace
# 2. Create the `tcss-admin` admin role under the `tcss` namespace
# 3. Bind the `tcss-admin` role to the `tcss` user
# 4. Create the `tcss-agent-secret` key and bind it to the `tcss-agent` service account
# 5. Create the `security-clusterrole` read-only cluster role
# 6. Bind the `security-clusterrole` role to the `tcss-agent` service account

---
apiVersion: v1
kind: Namespace
metadata:
  name: tcss


---
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: tcss
  name: tcss-admin
rules:
- apiGroups: ["extensions", "apps", ""]
  resources: ["*"]
  verbs: ["get", "list", "watch", "create", "update", "patch", "delete"]

---
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: tcss-admin-rb
  namespace: tcss
subjects:
- kind: User
  name: tcss
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: Role
  name: tcss-admin
  apiGroup: rbac.authorization.k8s.io


---
apiVersion: v1
kind: Secret
metadata:
  name: tcss-agent-secret
  namespace: tcss
  annotations:
    kubernetes.io/service-account.name: tcss-agent
type: kubernetes.io/service-account-token


---
apiVersion: v1
kind: ServiceAccount
metadata:
  name: tcss-agent
  namespace: tcss
secrets:
  - name: tcss-agent-secret
    namespace: tcss


---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: security-clusterrole
rules:
- apiGroups: ["", "v1"]
  resources: ["namespaces", "pods", "nodes"]
  verbs: ["get", "list"]
- apiGroups: ["apps"]
  resources: ["replicasets", "daemonsets", "deployments", "statefulsets"]
  verbs: ["get", "list"]
- apiGroups: ["batch"]
  resources: ["jobs", "cronjobs"]
  verbs: ["get", "list"]
- apiGroups: ["rbac.authorization.k8s.io"]
  resources: ["clusterroles", "clusterrolebindings"]
  verbs: ["get"]

---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: security-clusterrolebinding
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: security-clusterrole
subjects:
- kind: ServiceAccount
  name: tcss-agent
  namespace: tcss
- kind: User
  name: tcss
  apiGroup: rbac.authorization.k8s.io
```
3. Go to the configuration directory (/etc/origin/master/) and enter the following command to create a certificate.
```
# Create the `tcss.key` key for `User`
openssl genrsa -out tcss.key 2048

# Create the `tcss.csr` certificate signing request
openssl req -new -key tcss.key -out tcss.csr -subj "/O=K8s/CN=tcss"

# Sign the certificate and generate `tcss.crt`
openssl x509 -req -in tcss.csr -CA ca.crt -CAkey ca.key -CAcreateserial -out tcss.crt -days 365
```
4. Enter the following command to create a cluster configuration file.
```
# Create and set the cluster configuration. Here, the main server address must be a public network address that is accessible.
KUBECONFIG=/root/tcss.conf oc config set-cluster tcss --server=https://xx.xx.xx.xx:60002 --certificate-authority=/etc/origin/master/ca.crt --embed-certs=true --kubeconfig=/root/tcss.conf

# Create and set the user configuration
KUBECONFIG=/root/tcss.conf oc config set-credentials tcss --client-certificate=tcss.crt --client-key=tcss.key --embed-certs=true --kubeconfig=/root/tcss.conf

# Set the `context` configuration
KUBECONFIG=/root/tcss.conf oc config set-context tcss@tcss --cluster=tcss --user=tcss --kubeconfig=/root/tcss.conf

# Switch the `context` configuration
KUBECONFIG=/root/tcss.conf oc config use-context tcss@tcss --kubeconfig=/root/tcss.conf
```
5. Enter the following command to verify and upload the cluster configuration file.
```
KUBECONFIG=/root/tcss.conf oc -n tcss get pod
```
>?Run the above command. If the returned result displays a Pod or indicates that there are no relevant resources in the current namespace, the cluster configuration is available, and you just need to upload the file to `/root/tcss.conf`.

### Quick script[](id:yjjb2)
On the master node, you can use the following script code to quickly generate a cluster configuration file.
>? You need to install OpenSSL in the environment in advance.

```
#!/bin/bash

set -e;

# You need to set `API_SERVER` as the accessible address and port of the public network.
# API_SERVER=https://xx.xx.xx.xx:xxxx

# Set the following paths as needed
KUBECONFIG_TARGET=/root/tcss.conf
CA_FILE=/etc/kubernetes/ca.crt
CAKEY_FILE=/etc/kubernetes/ca.key
TCSS_TMPDIR=/tmp/tcss
KUBECTL_CMD=oc


if [ ! $API_SERVER ]; then
    echo "API_SERVER does not set.";
    exit 1;
fi
if ! which $KUBECTL_CMD ; then
    echo "$KUBECTL_CMD does not exist.";
    exit 1;
fi
if [ ! -f "$CA_FILE" ]; then
    echo "$CA_FILE does not exist.";
    exit 1;
fi
if [ ! -f "$CAKEY_FILE" ]; then
    echo "$CAKEY_FILE does not exist.";
    exit 1;
fi
if [ ! -d $TCSS_TMPDIR ]; then
    mkdir -p $TCSS_TMPDIR;
fi

cat <<EOF  > $TCSS_TMPDIR/tcss_res.yaml
---
apiVersion: v1
kind: Namespace
metadata:
  name: tcss

---
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: tcss
  name: tcss-admin
rules:
- apiGroups: ["extensions", "apps", ""]
  resources: ["*"]
  verbs: ["get", "list", "watch", "create", "update", "patch", "delete"]

---
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: tcss-admin-rb
  namespace: tcss
subjects:
- kind: User
  name: tcss
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: Role
  name: tcss-admin
  apiGroup: rbac.authorization.k8s.io

---
apiVersion: v1
kind: Secret
metadata:
  name: tcss-agent-secret
  namespace: tcss
  annotations:
    kubernetes.io/service-account.name: tcss-agent
type: kubernetes.io/service-account-token

---
apiVersion: v1
kind: ServiceAccount
metadata:
  name: tcss-agent
  namespace: tcss
secrets:
  - name: tcss-agent-secret
    namespace: tcss

---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: security-clusterrole
rules:
- apiGroups: ["", "v1"]
  resources: ["namespaces", "pods", "nodes"]
  verbs: ["get", "list"]
- apiGroups: ["apps"]
  resources: ["replicasets", "daemonsets", "deployments", "statefulsets"]
  verbs: ["get", "list"]
- apiGroups: ["batch"]
  resources: ["jobs", "cronjobs"]
  verbs: ["get", "list"]
- apiGroups: ["rbac.authorization.k8s.io"]
  resources: ["clusterroles", "clusterrolebindings"]
  verbs: ["get"]


---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: security-clusterrolebinding
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: security-clusterrole
subjects:
- kind: ServiceAccount
  name: tcss-agent
  namespace: tcss
- kind: User
  name: tcss
  apiGroup: rbac.authorization.k8s.io
EOF

# echo "generate tcss resource file ($TCSS_TMPDIR/tcss_res.yaml) success."

$KUBECTL_CMD apply -f $TCSS_TMPDIR/tcss_res.yaml;
$KUBECTL_CMD adm policy add-scc-to-user privileged -n tcss -z tcss-agent;
$KUBECTL_CMD adm policy add-scc-to-user hostaccess -n tcss -z tcss-agent;
$KUBECTL_CMD adm policy add-scc-to-user privileged tcss;
$KUBECTL_CMD adm policy add-scc-to-user hostaccess tcss;
oc adm policy add-cluster-role-to-user cluster-reader tcss;

# Create the `tcss.key` key for `User`
openssl genrsa -out $TCSS_TMPDIR/tcss.key 2048
# Create the `tcss.csr` certificate signing request
openssl req -new -key $TCSS_TMPDIR/tcss.key -out $TCSS_TMPDIR/tcss.csr -subj "/O=K8s/CN=tcss"
# Sign the certificate and generate `tcss.crt`
openssl x509 -req -in $TCSS_TMPDIR/tcss.csr -CA $CA_FILE -CAkey $CAKEY_FILE -CAcreateserial -out $TCSS_TMPDIR/tcss.crt -days 365

# Create and set the cluster configuration
KUBECONFIG=$KUBECONFIG_TARGET $KUBECTL_CMD config set-cluster tcss --server=$API_SERVER --certificate-authority=$CA_FILE --embed-certs=true --kubeconfig=$KUBECONFIG_TARGET
# Create and set the user configuration
KUBECONFIG=$KUBECONFIG_TARGET $KUBECTL_CMD config set-credentials tcss --client-certificate=$TCSS_TMPDIR/tcss.crt --client-key=$TCSS_TMPDIR/tcss.key --embed-certs=true --kubeconfig=$KUBECONFIG_TARGET
# Set the `context` configuration
KUBECONFIG=$KUBECONFIG_TARGET $KUBECTL_CMD config set-context tcss@tcss --cluster=tcss --user=tcss --kubeconfig=$KUBECONFIG_TARGET
# Switch the `context` configuration
KUBECONFIG=$KUBECONFIG_TARGET $KUBECTL_CMD config use-context tcss@tcss --kubeconfig=$KUBECONFIG_TARGET

echo "generate KUBECONFIG file success. $KUBECONFIG_TARGET"
```


