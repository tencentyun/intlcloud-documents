## Overview

### Add-on Description
TCR Addon is a plug-in provided by the Tencent Container Registry (TCR) service for private-network and Secret-free pulling of container images. After this plug-in is installed in a TKE cluster, cluster nodes can pull container images from Enterprise Edition instances over the private network, without the need for explicit configuration of ImagePullSecret in the cluster resource YAML file. This plug-in can accelerate image pulling in TKE clusters and simplify image configuration.
>?
>- The TKE cluster version must be v1.10.x or later. We recommend that you use this add-on in TKE v1.12.x or later.
- The startup parameters of the Kubernetes `controller manager` component must contain `authentication-kubeconfig` and `authorization-kubeconfig` (enabled by default in TKE v.12.x).


### Kubernetes objects deployed in a cluster

| Name | Type | Resource Amount | Namespace |
| ---------------------------------------------- | ------------------------------ | ---------------------- | -------------------- |
| tcr-assistant-system | Namespace | 1 | - |
| tcr-assistant-manager-role | ClusterRole | 1 | - |
| tcr-assistant-manager-rolebinding | ClusterRoleBinding | 1 | - |
| tcr-assistant-leader-election-role | Role | 1 | tcr-assistant-system |
| tcr-assistant-leader-election-rolebinding | RoleBinding | 1 | tcr-assistant-system |
| tcr-assistant-webhook-server-cert | Secret | 1 | tcr-assistant-system |
| tcr-assistant-webhook-service | Service | 1 | tcr-assistant-system |
| tcr-assistant-validating-webhook-configuration | ValidatingWebhookConfiguration | 1 | tcr-assistant-system |
| imagepullsecrets.tcr.tencentcloudcr.com | CustomResourceDefinition | 1 | tcr-assistant-system |
| tcr.ips* | ImagePullSecret CRD | (2-3) | tcr-assistant-system |
| tcr.ips* | Secret | (2-3)*{Namespace No.} | tcr-assistant-system |
| tcr-assistant-controller-manager | Deployment | 1 | tcr-assistant-system |
| updater-config | ConfigMap | 1 | tcr-assistant-system |
| hosts-updater | DaemonSet | {Node No.} | tcr-assistant-system |

### Component resource usage

| Component | Resource Usage | Instance Quantity |
| -------------------------------- | ----------------------- | ---------- |
| tcr-assistant-controller-manager | CPU：100m memory：30Mi  | 1          |
| hosts-updater                    | CPU：100m memory：100Mi | Number of worker nodes |


## Use Cases

### Pulling images without a Secret

For a Kubernetes cluster to pull private images, you must create access credential Secret resources, configure the ImagePullSecret attribute in the YAML file of the resources, and explicitly specify the created Secret. The overall configuration process is complicated, and image pull will fail if the Secret is not configured or the specified Secret is incorrect.
In face of this problem, you can install the TCR add-on in the cluster. The add-on automatically obtains the access credential of the specified TCR Enterprise Edition instance and delivers it to the specified namespace of the TKE cluster. When using the YAML file to create or update resources, you do not need to configure ImagePullSecret. Instead, the cluster automatically uses the delivered access credential to pull images from the TCR Enterprise Edition instance.

### Pulling images over the private network
The add-on automatically creates a DaemonSet workload, host-updater, which is used to update the host configuration of nodes in the cluster. Note that this configuration is only recommended for test scenarios. For resolving, you can use the private network linkage provided by TCR, PrivateDNS, or your own DNS service. 

## Limits
- **For use cases of secret-free image pulling**:
 - Users must have the permission to obtain the access credential of the specified TCR Enterprise Edition instance, that is, the permission to call the CreateInstanceToken API. We recommend that users with TCR admin permissions configure this add-on.
 - After the add-on is installed and takes effect, do not repeatedly specify ImagePullSecret in the resource YAML file. Otherwise, nodes may use the incorrect image pull access credential, leading to pull failures.

## Directions
1. Select an associated instance: select an existing TCR Enterprise Edition instance under the current logged-in account and confirm that the current logged-in user has the permission to create a long-term access credential for the instance. If you need to create a new Enterprise Edition instance, create it in the region where the current cluster is located.
2. Configure secret-free pulling (enabled by default): you can choose to issue the access credential automatically for the current user, or specify the username and password,. You can also configure the namespace and ServiceAccount for which you want to enable Secret-free pulling.  We recommend that you keep the default configuration to make sure this feature works on the new namespace.
3. Configure private network resolving (advanced feature): make sure that there is already a private network linkage between the cluster and the associated TCR instance, and **Private Network Resolving** is enabled. Note that this configuration is only recommended for test scenarios. For resolving, you can use the private network linkage provided by TCR, PrivateDNS, or your own DNS service.
4. After the TCR add-on is created, if you need to modify its configuration, delete the add-on and reconfigure and reinstall it.
>! When the TCR add-on is deleted, the created dedicated access credential is not automatically deleted. You can go to the TCR console to manually disable or delete the credential.

## How It Works
### Overview
TCR Assistant helps you implement the auto-process of deploying  k8s `imagePullSecret` to any namespace, and associate it with the `ServiceAccount` of the namespace. If you do no **explicitly specify** the `imagePullSecret` and `serviceAccount` when create the workload, K8s will try find the matched `imagePullSecret` from the `ServiceAccount` named `default` under the namespace.

### Glossary

| Name            | Alias      | Description                                                                                                   |
| :-------------- | :-------- | :----------------------------------------------------------------------------------------------------- |
| ImagePullSecret | ips, ipss | The CRD defined by TCR Assistant. It’s used to store the username and password of the image repository, and issue the target `Namespace` and `ServiceAccount`. |


### How it works

![](https://qcloudimg.tencent-cloud.cn/raw/0d699c0f710b3dee883773d4dc0749b5.png)

TCR Assistant is a classic K8s Operator. Upon deployment of TCR Assistant, the CRD object `imagepullsecrets.tcr.tencentcloudcr.com` is created automatically. This CRD’s `kind` is `ImagePullSecret`, and its version is `tcr.tencentcloudcr.com/v1`, with the alias as `ips` or `ipss`.

TCR Assistant keeps watching the resource status of `Namespace` and `ServiceAccount` in the cluster. When there are resource changes, it checks whether the changes match the rules set in `ImagePullSecret`. If yes,  it automatically deploys the Secret required to pull the **private image repository**. TCR Assistant is usually deployed in a K8s cluster, and accesses K8s master API in `in cluster` mode.

### Creating CRD resources
When TCR Assistant is deployed, the Secret used to pull TCR image is not deployed in the target K8s cluster. You need to create `ImagePullSecret` using kubectl or Client Go.

```bash
# Create ImagePullSecret resource
$ kubectl create -f allinone/imagepullsecret-sample.yaml

imagepullsecret.tcr.tencentcloudcr.com/imagepullsecret-sample created
```

`ImagePullSecret` resource sample file (allinone/imagepullsecret-sample.yaml): 
```yaml
apiVersion: tcr.tencentcloudcr.com/v1
kind: ImagePullSecret
metadata:
  name: imagepullsecret-sample
spec:
  namespaces: "*"
  serviceAccounts: "*"
  docker:
    username: "100012345678"
    password: tcr.jwt.token
    server: fanjiankong-bj.tencentcloudcr.com
```

Description of `ImagePullSecret` spec fields: 
| Field            | Description                       | Remarks                                                                                                                                        |
| --------------- | -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| namespaces      | `NameSpace` matching rule       | Match any namespace: `*` or blank; Match any of multiple namespaces: enter the resource names and separate them with `,`. **Note**: Expressions are not supported. Please enter the exact resource name. |
| serviceAccounts      | `serviceAccounts` matching rule       | Match any namespace: `*` or blank; Match any of multiple namespaces: enter the resource names and separate them with `,`. **Note**: Expressions are not supported. Please enter the exact resource name. |
| docker.server   | Image repository domain name| Please enter only the repository domain name                                                                                                                             |
| docker.username | Image repository username             | Make sure the user has all the required permissions                                                                                                  |
| docker.password | Password of the image repository username |


After the creation, you can run the following command to check execution result of TCR Assistant: 
```bash
# List ImagePullSecret information
$ kubectl get ipss
NAME                     NAMESPACES   SERVICE-ACCOUNTS   SECRETS-DESIRED   SECRETS-SUCCESS
imagepullsecret-sample   *            *                  10                10

# Check details
$  kubectl describe ipss
Name:         imagepullsecret-sample
Namespace:
Labels:       <none>
Annotations:  <none>
API Version:  tcr.tencentcloudcr.com/v1
Kind:         ImagePullSecret
Metadata:
  Creation Timestamp:  2021-12-01T06:47:34Z
  Generation:          1
    Manager:      kubectl-client-side-apply
    Operation:    Update
    Time:         2021-12-01T06:47:34Z
    API Version:  tcr.tencentcloudcr.com/v1
    Manager:         manager
    Operation:       Update
    Time:            2021-12-01T06:47:38Z
  Resource Version:  30389349
  UID:               2109f384-240b-405c-9ce8-73ce938a7c2f
Spec:
  Docker:
    Password:        tcr.jwt.token
    Server:          fanjiankong-bj.tencentcloudcr.com
    Username:        100012345678
  Namespaces:        *
  Service Accounts:  *
Status:
  S As Desired:  47
  S As Success:  1
  Secret Update Successful:
    Namespaced Name:  kube-public/tcr.ipsimagepullsecret-sample
    Updated At:       2021-12-01T06:47:36Z
    Namespaced Name:  devtools/tcr.ipsimagepullsecret-sample
    Updated At:       2021-12-01T06:47:36Z
    Namespaced Name:  demo/tcr.ipsimagepullsecret-sample
    Updated At:       2021-12-01T06:47:36Z
    Namespaced Name:  kube-system/tcr.ipsimagepullsecret-sample
    Updated At:       2021-12-01T06:47:36Z
    Namespaced Name:  tcr-assistant-system/tcr.ipsimagepullsecret-sample
    Updated At:       2021-12-01T06:47:36Z
    Namespaced Name:  kube-node-lease/tcr.ipsimagepullsecret-sample
    Updated At:       2021-12-01T06:47:36Z
    Namespaced Name:  cert-manager/tcr.ipsimagepullsecret-sample
    Updated At:       2021-12-01T06:47:36Z
    Namespaced Name:  default/tcr.ipsimagepullsecret-sample
    Updated At:       2021-12-01T06:47:36Z
    Namespaced Name:  afm/tcr.ipsimagepullsecret-sample
    Updated At:       2021-12-01T06:47:37Z
    Namespaced Name:  lens-metrics/tcr.ipsimagepullsecret-sample
    Updated At:       2021-12-01T06:47:37Z
  Secrets Desired:    10
  Secrets Success:    10
  Service Accounts Modify Successful:
    Namespaced Name:  default/default
    Updated At:       2021-12-01T06:47:38Z
Events:               <none>

```

>!to update the `Secret` resource deployed by TCR Assistant, you don’t need to delete and rebuild `ImagePullSecret`. All you need to do is to edit the `docker.username` and `docker.password` fields using the command below: 
>
```bash
$ kubectl edit ipss imagepullsecret-sample
```

#### Namespace updates
When TCR Assistant detects new K8s `Namespace`, it checks whether the name of the resource matches the `namespaces` field of `ImagePullSecret`. If the names are not matched, it goes to the next step. If the names are matched, K8s API is invoked to create a `Secret` resource, and the `Secret` name is added to the `imagePullSecrets` of `ServiceAccount`. See below for examples: 

```
# Check the Secret automatically deployed under newns
$ kubectl get secrets -n newns
NAME                            TYPE                                  DATA   AGE
tcr.ipsimagepullsecret-sample   kubernetes.io/dockerconfigjson        1      7m2s
default-token-nb5vw             kubernetes.io/service-account-token   3      7m2s

# Check the Secret automatically associated with the `ServiceAccount` resource name `default` under newns
$ kubectl get serviceaccounts default -o yaml -n newns
apiVersion: v1
imagePullSecrets:
- name: tcr.ipsimagepullsecret-sample
kind: ServiceAccount
metadata:
  creationTimestamp: "2021-12-01T07:09:56Z"
  name: default
  namespace: newns
  resourceVersion: "30392461"
  uid: 7bc67144-3685-4666-ba41-b1447bbbaa38
secrets:
- name: default-token-nb5vw

```

#### ServiceAccount updates
When TCR Assistant detects new K8s `ServiceAccount`, it checks whether the name of the resource matches the `serviceAccounts` field of `ImagePullSecret`. If the names are **not matched**, it goes to the next step. If the names are matched, K8s API is invoked to create or update `Secret` resource, and the `Secret` name is added to the `imagePullSecrets` field of `ServiceAccount`. See below for examples: 

```bash
# Create ServiceAccount resource under newns
$ kubectl create sa kung -n newns
serviceaccount/kung created

# Check the Secret automatically associated with the newly-created `ServiceAccount` resource name `kung` under newns
$ kubectl get serviceaccounts kung -o yaml -n newns
apiVersion: v1
imagePullSecrets:
- name: tcr.ipsimagepullsecret-sample
kind: ServiceAccount
metadata:
  creationTimestamp: "2021-12-01T07:19:12Z"
  name: kung
  namespace: newns
  resourceVersion: "30393760"
  uid: e236829e-d88e-4feb-9e80-5e4a40f2aea2
secrets:
- name: kung-token-fljt8
```



