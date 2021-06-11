## Overview

### Add-on description
The TCR add-on is a plug-in provided by the Tencent Container Registry (TCR) service for the private-network and secret-free pulling of container images. After the TCR add-on is installed in a TKE cluster, nodes in the cluster can pull container images from Enterprise Edition instances over the private network, without the need for explicit configuration of ImagePullSecret in the cluster resource YAML file. The TCR add-on can accelerate image pulling in TKE clusters and simplify image configuration.
>?
>
>- The TKE cluster version must be v1.10.x or later. We recommend that you use this plug-in in TKE v1.12.x or later.
>- The startup parameters of the Kubernetes `controller manager` component must contain `authentication-kubeconfig` and `authorization-kubeconfig` (enabled by default in TKE v.12.x).


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
| tcr-assistant-controller-manager | CPU: 100M, memory: 30Mi | 1 |
| hosts-updater | CPU: 100M, memory: 100Mi | Number of worker nodes |


## Use Cases

### Pulling images without a secret

Before a Kubernetes cluster pulls private images, you must create access credential secret resources, configure the ImagePullSecret attribute in the YAML file of the resources, and explicitly specify the created secret. The overall configuration process is complicated, and image pull will fail if ImagePullSecret is not configured or the specified secret is incorrect.
To solve the preceding problems, you can install the TCR add-on in the cluster. The add-on automatically obtains the access credential of the specified TCR Enterprise Edition instance and delivers it to the specified namespace of the TKE cluster. When using the YAML file to create or update resources, you do not need to configure ImagePullSecret. The cluster automatically uses the delivered access credential to pull images from the TCR Enterprise Edition instance.

### Pulling images over the private network

When pulling images, a Kubernetes cluster accesses the TCR service over the node network. If the cluster accesses the TCR service through public network images, a public network traffic fee is incurred, the pull speed is slow, and network security risks exist. Currently, TCR supports both public-network access and private-network access. You can use the TCR console to connect to VPCs that require private-network access. After configuration, TKE clusters in the VPCs can access private repositories in TCR over the private network. To ensure that cluster nodes can normally resolve TCR-exclusive instance domain names into private-network access addresses, you need to configure Host on the nodes or use a self-built DNS service.
To simplify private-network resolution configuration, you can install the TCR add-on in the cluster. The add-on will automatically configure private-network resolution for the domain names of the specified TCR Enterprise Edition instance for cluster nodes. The add-on also supports the default domain name, dedicated private-network domain names, and custom domain names.

## Limits
- **For use cases of secret-free image pulling**:
 - Users must have the permission to obtain the access credential of the specified TCR Enterprise Edition instance, that is, the permission to call the CreateInstanceToken API. We recommend that users with TCR admin permissions configure this add-on.
 - After the add-on is installed and takes effect, do not repeatedly specify ImagePullSecret in the resource YAML file. Otherwise, nodes may use the incorrect image pull access credential, leading to pull failures.
- **For use cases of private-network image pulling**:
 - First, use the TCR console to connect the VPC of the cluster to the specified TCR instance and check that the private network access link is normal. Then, install and configure this add-on.
 - Custom domain names only support the use of tencentcloudcr.com as the root domain name. After configuration, clusters cannot access the specified TCR instance over the public network.


## Usage
1. Select an associated instance: select an existing TCR Enterprise Edition instance under the current account and confirm that the current user has the permission to create a long-term access credential for the instance. If you need to create a new Enterprise Edition instance, create it in the region where the current cluster is located.
2. Configure secret-free pulling (enabled by default): configure the namespace and ServiceAccount for which Secret-free pulling will take effect. For the detailed configuration, see [Parameter description](#ParameterDescription). We recommend that you use the default configuration to prevent the problem where this feature is unavailable to new namespaces.
3. Configure private network resolution (optional feature): confirm that a private network access link has been established between the cluster and associated TCR instance and enable the private network resolution feature. If you have manually modified the cluster node Host or used a self-built DNS service to implement private network resolution, you can disable this feature.
>! After this feature is enabled, private network access domain names will be forcibly resolved to the private network access addresses provided by the associated TCR instance and cannot be used for public network access.
4. After the TCR add-on is created, if you need to modify its configuration, delete the add-on and reconfigure and reinstall it.
>! When the TCR add-on is deleted, the created dedicated access credential is not automatically deleted. You can go to the TCR console to manually disable or delete the credential.





## Directions
1. Log in to the [Tencent Kubernetes Engine console](https://console.cloud.tencent.com/tke2) and click **Cluster** in the left sidebar.
2. On the "Cluster Management" page, click the ID of the target cluster to go to the cluster details page.
3. In the left sidebar, click **Add-on Management** to go to the "Add-on List" page.
4. On the "Add-on List" page, click **Create**, On the "Create an Add-on" page that appears, select **TCR**.
5. Choose **Parameter Configuration**. In the displayed "TCR Add-on Parameter Settings" window, configure relevant parameters, as shown in the figure below: 
![](https://main.qcloudimg.com/raw/b6e472fa701ae6b31eb82bff1ffd7d67.png)
6. Click **OK**.





## Related Information
<span id="ParameterDescription"></span>
### Parameter description

- **Associated Instance**: indicates the TCR Enterprise Edition instance to be used by the current cluster. The plug-in automatically configures the access credential of the registry instance and private-network domain name resolution for the current cluster.
- **Configuration for secret-free pulling**:
  - **Namespace**: indicates the namespace for which secret-free pulling takes effect. You can specify one or more namespaces or directly use `*` to specify all namespaces (including new namespaces) in the cluster. The default configuration is `*`, indicating that secret-free pulling will take effect for all namespaces in the current cluster. After the TCR add-on is installed, you can view the secret automatically created by the add-on in the specified namespace.
  - **ServiceAccount**: indicates the ServiceAccount for which secret-free pulling takes effect. You can specify one or more ServiceAccounts or directly use `_` to specify all ServiceAccounts (including new ServiceAccounts) in the namespace. The default configuration is `_`, indicating that secret-free pulling will take effect for all ServiceAccounts in the specified namespace of the current cluster.
  - **Access Credential Description**: after secret-free pulling is enabled for a cluster, a long-term access credential dedicated to the cluster will be automatically created in the associated Enterprise Edition instance. Its description explains the use case of the access credential. The default description is "TKE cluster (cls-xxxxxxx) dedicated access credential", where cls-xxxxxxx is the unique ID of the current cluster.
- **Configuration for private-network access**:
  - **Private Network Access Link**: to access the associated TCR Enterprise Edition instance from a cluster over the private network, you need to use the TCR console to connect the VPC where the cluster is located with the associated instance to establish a private-network access link between them. The value of this parameter indicates whether the current cluster has established a normal private-network access link with the associated instance. If not, go to the TCR console, choose **Access Control** > **Private Network Access**, and connect the VPC with the associated instance.
  - **Enable Private Network Resolution**: this is an optional feature. If you have established a private-network access link between the current cluster and the associated TCR instance, you can manually configure the node Host or use the self-built DNS service to implement private-network resolution. Alternatively, you can enable this feature, and the add-on will automatically configure the private network resolutions of domain names of the associated TCR instance for existing and new nodes in the cluster.
  - **Private Network Access Domain Names**: the TCR Enterprise Edition instance provides dedicated access domain names. You can use the default domain name, private-network dedicated domain names, or custom domain names in a cluster. The private network resolution configuration of these domain names takes effect only in the cluster. For custom domain names, the root domain name tencentcloudcr.com must be used.
