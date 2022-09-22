## Overview
Tencent Cloud TKE offers two ways to create clusters: [creating a cluster with a template](#TemplateCreation) and [customizing a cluster](#CustomClusterCreation). This document describes how to create clusters and all necessary resources, such as VPCs, subnets, and security groups, using templates and custom configurations.

## Prerequisites

Before creating a cluster, you need to complete the following preparations:
- [Sign up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and complete [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).
- When you log in to the [TKE console](https://console.cloud.tencent.com/tke2) for the first time, you need to grant the current account TKE permissions for operating on CVMs, CLBs, CBS, and other cloud resources. For more information, see [Description of Role Permissions Related to Service Authorization](https://intl.cloud.tencent.com/document/product/457/37808).
- To create a container cluster whose network type is virtual private cloud (VPC), you need to [create a VPC](https://intl.cloud.tencent.com/document/product/215/31805) in the target region and [create a subnet](https://intl.cloud.tencent.com/document/product/215/31806) in the target availability zone under the VPC.
- If you do not use the default security group, you need to [create a security group](https://intl.cloud.tencent.com/document/product/213/34271) in the target region and add a security group rule that meets your business requirements.
- To bind a SSH key pair when creating a Linux instance, you need to [create a SSH key](https://intl.cloud.tencent.com/document/product/213/16691) for the target project.
- When you create a cluster, you will use the resources such as VPCs, subnets, and security groups. Each region has a resource quota. For more information on resource quotas, refer to [Quota Limits for Cluster Purchase](https://intl.cloud.tencent.com/document/product/457/9087).





## Directions

### Creating a cluster with a template[](id:TemplateCreation)

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cluster** in the left sidebar.
2. On the **Cluster Management** page, click **Create with a template** above the cluster list.
![](https://main.qcloudimg.com/raw/22e1a2aa51008198b65c81dd08675019.png)
3. Multiple templates are provided for creating managed clusters, self-deployed clusters and elastic clusters. You can choose a template based on your actual requirements.
 - **Managed cluster**: If you create a Kubernetes managed cluster, you do not need to purchase and manage the cluster master node and only need to purchase worker node resources to deploy business applications.
 - **Self-deployed cluster**: If you create a self-deployed Kubernetes cluster, you need to purchase and manage the master and worker nodes of the cluster. You will have all the management and operation permissions of the cluster.
 - **Elastic cluster**: If you create a serverless Kubernetes cluster, you do not need to manage any node resources of the cluster and can quickly deploy business applications.
4. This document uses the **Basic cluster** template under a managed cluster as an example. Select the **Basic cluster** and go to the **Create basic cluster** page.
>?When using a cluster template to create a cluster, all configuration items adopt their default values. You can directly click **Next** or refer to the directions in [Customizing a cluster](#CustomClusterCreation) to customize the configuration.
>
5. Click **Complete**.



### Customizing a cluster[](id:CustomClusterCreation)

#### 1. Enter the cluster information

1. [](id:step1)Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cluster** in the left sidebar.
2. On the "Cluster Management" page, click **Create** above the cluster list.
3. On **Create cluster** page, configure the basic information of the cluster.
![](https://main.qcloudimg.com/raw/31e3fa0551850812cacef99fd6d75cf9.png)
 - **Cluster name**: The name of the cluster to be created, with a length up to 60 characters.
 - **Project of new resource**: Select a project as needed. The newly added resources will be automatically assigned to this project.
 - **Kubernetes version**: Multiple Kubernetes versions are available. For feature comparison between different versions, see [Supported Versions of the Kubernetes Documentation](https://kubernetes.io/docs/home/supported-doc-versions/).
 - **Runtime components**: Select **docker** or **containerd**. For more information, see [How to Choose Containerd and Docker](https://intl.cloud.tencent.com/document/product/457/31088).
 - **Region**: The region where the cluster to be created is located. We recommend that you select the region closest to you to help minimize access latency and improve the download speed.
 - **Cluster network**: Assigns IP addresses that are within the node network address range to CVMs in the cluster. For details, see [Network Settings for Containers and Nodes](https://intl.cloud.tencent.com/document/product/457/38966).
 - **Container network add-on**: **GlobalRouter** and **VPC-CNI** network modes are provided. For more information, see [Container Network Overview](https://intl.cloud.tencent.com/document/product/457/38966).
 - **Container network**: Assigns IP addresses that are within the container network address range to containers in the cluster. For details, see [Network Settings for Containers and Nodes](https://intl.cloud.tencent.com/document/product/457/38966).
 - **Operating system**: Select the operating system based on your requirements.
 - **Cluster description**: Enter information about the cluster, which will be displayed on the **Cluster information** page.
 - **Advanced settings** (optional):
    - **Tencent Cloud tags**: After binding tags to the cluster, you can categorize the resources. For more information, see [Querying Resources by Tag](https://intl.cloud.tencent.com/document/product/651/32582).   
    - **Deletion protection**: When it's enabled, the cluster will not be deleted by mis-operation in the console or by the API.
    - **Kube-proxy proxy mode**: Select iptables or ipvs. IPVS mode is applicable to large-scale services. You cannot disable it once it is enabled. For details, refer to [Enabling IPVS for a Cluster](https://intl.cloud.tencent.com/document/product/457/30641).
    - **Custom parameters**: Specify the custom parameters to configure the cluster.
    - **Runtime version**: Select the version of the container runtime component.
4. Click **Next**.

#### 2. Select a model
On the **Select model** page, confirm the billing mode, select an AZ and the corresponding subnet, and confirm the node model.
1. Select *Add node** or **Existing nodes** for **Node source**.
<dx-tabs>
::: Add node
Create a cluster by adding nodes, i.e., CVM instances. The details are as follows:

- **Cluster type**: You can select **Managed cluster** or **Self-deployed cluster**.
	- Managed cluster: The Master and Etcd of the Kubernetes cluster will be managed and maintained by Tencent Cloud.
	- Self-deployed cluster: The Master and Etcd of the Kubernetes cluster will be deployed on the CVM instance you purchased.

- **Cluster specification:** Select an appropriate cluster specification as needed. For more information, see [Purchase Instructions](https://intl.cloud.tencent.com/document/product/457/45158). You can adjust the cluster specification manually, or enable Auto Cluster Upgrade to have it adjusted automatically.

- **Billing mode**: **Pay-as-you-go** is supported. For more information, see [Billing Plans](https://intl.cloud.tencent.com/document/product/213/2180).

- **Worker configurations**: If you select **Add node** for **Node source** and **Managed cluster** for **Cluster type**, all configuration items in this module are set to the default values. You can modify them as needed.
   - **Availability zone**: You can select multiple availability zones at the same time to deploy your Master or Etcd nodes to ensure higher availability of the cluster.
   - **Node network**: You can select multiple subnet resources at the same time to deploy your Master or Etcd nodes to ensure higher availability of the cluster.
   - **Model**: Select a model with more than four CPU cores. For more information, see [Instance Types](https://intl.cloud.tencent.com/document/product/213/11518) and [Customizing Linux CVM Configurations](https://intl.cloud.tencent.com/document/product/213/10517).
      - **System disk**: The default value is **HDD cloud disk - 50 GB**. You can select local disk, HDD cloud disk, SSD cloud disk, or premium cloud disk based on your actual model. For details, see [Storage Overview](https://intl.cloud.tencent.com/document/product/213/4952).
      - **Data disk**: As it is not recommended to deploy other applications in the Master and Etcd nodes, no data disk is configured for them by default. You can purchase one and add it if needed.
      - **Public network bandwidth**: Select **Assign free public IP** and the system will assign a public IP address for free. Two billing methods are available. For more information, see [Public Network Billing](https://intl.cloud.tencent.com/document/product/213/10578).
      - **Node name**: The name of the computer in the OS (the node name displayed by running the `kubectl get nodes` command`). It is a cluster attribute. The node name can be named in the following two modes:
        - **Auto-generated**: The node hostname defaults to the private IP of the node.
        - **Custom name**: You can use sequential numbering or custom format string. It can contain 2-60 characters, including lower-case letters, numbers, hyphens ("-") and periods ("."). Symbols cannot be placed at the beginning nor end, and cannot be used consecutively. For more naming rules, see [Batch Sequential Naming or Pattern String-Based Naming](https://intl.cloud.tencent.com/document/product/213/32020).
>!Due to the naming restriction of kubernetes node, you can only use the lower-case letters when customizing the hostname, for example, 'cvm {R:13}-big{R:2}-test'.
>
        - **Instance name**: The CVM instance name displayed in the console, which is determined by the naming mode of the hostname.
         - When the node hostname is automatically generated, it supports sequential numbering or custom format for multiple instances. Up to 60 characters are allowed. The instance name is automatically generated by default in the format of `tke_cluster id_worker`.
         - When the node hostname is customized, the instance name is the same as the hostname, without the need to reconfigure it.
      -  **CVM quantity**: Set the number of instances as needed.
>? If **Self-deployed cluster** is selected for **Cluster type**, you can also refer to “Worker configurations” to set the Master and Etcd nodes. Deploy at least three instances, which can be in different AZs.
>


:::
::: Existing nodes [](id:UseExistingCVMCreateCluster)
Create a cluster using the existing nodes (i.e., CVM instances). The details are as follows:
>!
> - The selected CVMs will be reinstalled and all data in the system disk will be cleared.
> - The selected CVMs will be migrated to the project of the cluster. All related security groups will be unbound. You need to bind them manually again.
>- If you set the data disk mounting parameters when configuring the CVM, this parameter will be applied to **all Master and Worker nodes**. For more information, see the **Mount data disk** section in [Adding an existing node](https://intl.cloud.tencent.com/document/product/457/30652).
>

- **Cluster type**: You can select **Managed cluster** or **Self-deployed cluster**.
	- Managed cluster: The Master and Etcd of the Kubernetes cluster will be managed and maintained by Tencent Cloud.
	- Self-deployed cluster: The Master and Etcd of the Kubernetes cluster will be deployed on the CVM instance you purchased.

- **Cluster specification:** Select an appropriate cluster specification as needed. For more information, see [Purchase Instructions](https://intl.cloud.tencent.com/document/product/457/45158). You can adjust the cluster specification manually, or enable Auto Cluster Upgrade to have it adjusted automatically.

- **Worker configurations**: Select the existing CVMs based on actual needs.

:::
</dx-tabs>
2. Click **Next** to start [configuring a CVM instance](#ConfigureCVM).

[](id:ConfigureCVM)
#### 3. Configure CVM
1. In the "CVM configuration" step, configure a CVM based on the following information.
![](https://main.qcloudimg.com/raw/24a166447e301672141a4f2257d7a206.png)
 - **Container directory**: Select this option to set up the container and image storage directory. We recommend that you store to the data disk, such as `/var/lib/docker`.
 - **Security group**: The security group works as a firewall to control network access of the CVM. The following settings are supported:
    - Create and bind the default security group. You can preview the default security group rules.
    - Add a security group to configure custom security group rules according to your actual needs.
    For details, see [TKE Security Group Settings](https://intl.cloud.tencent.com/document/product/457/9084).
 - **Login method**: Three login methods are available.
    - **SSH key pair**: A key pair is a pair of parameters generated by using an algorithm. Using a key pair to log in to a CVM instance is more secure than using regular passwords. For more information, see [SSH Key](https://intl.cloud.tencent.com/document/product/213/6092).
    - **Random password**: The system sends an automatically generated password to your [Message Center](https://console.cloud.tencent.com/message). 
    - **Custom password**: Set a password as prompted.
  - **Security services**: Free DDoS, Web Application Firewall (WAF) and Cloud Workload Protection Platform (CWPP) are activated by default. For more information, see [Cloud Workload Protection](https://intl.cloud.tencent.com/products/cwpp).
  - **Cloud monitor**: Free monitoring, analysis, and alarms are activated by default, and components are installed to obtain CVM monitoring metrics. For more information, see [Cloud Monitor](https://intl.cloud.tencent.com/products/cm).
2. (Optional) Click **Advanced settings** to view or configure more information.
![](https://main.qcloudimg.com/raw/f6bd03236aac6a6c56557dced60fda02.png)
 - **CAM role**: You can bind all the nodes created this time to the same CAM role, and grant the authorization policy bound to the role to the nodes. For more information, see [Managing Roles](https://intl.cloud.tencent.com/document/product/213/38290).
 - **Node launch configuration**: Specify custom data to configure the node, that is, to run the configured script when the node is started up. You need to ensure the reentrant and retry logic of the script. The script and its log files can be viewed at the node path: `/usr/local/qcloud/tke/userscript`.
 - **Cordon**: After you select **Cordon this node**, new Pods cannot be scheduled to this node. You can uncordon the node manually, or execute the [uncordon command](https://intl.cloud.tencent.com/document/product/457/30654) in custom data as needed.
  - **Label**: Click **Add** to customize the label. The label set here will be automatically added to the initial nodes of the cluster, and is used to filter and manage nodes in the future.
3. Click **Next**.




#### 4. Configure add-ons
1. Configure add-ons based on the following information.
![](https://main.qcloudimg.com/raw/5d7dc6f9da2bcc56961eda8d3cfc4a68.png)
 - **Add-ons**: You can select the add-ons such as storage, monitor, and image as needed. For more information, see [Add-on Overview](https://intl.cloud.tencent.com/document/product/457/33988).
 - **Log service**: The cluster auditing is enabled by default. For more information, see [Cluster Audit](https://intl.cloud.tencent.com/document/product/457/38338).
2. Click **Next**.


#### 5. Confirm the information
On the **Confirm information** page, confirm the selected configuration information and billing mode for the cluster, and click **Complete**.


### Viewing the cluster
You can view clusters that have been created in the [cluster list](https://console.cloud.tencent.com/tke2/cluster?rid=1). You can click the cluster ID to enter the details page, and then view the cluster, node, and network information on the "Basic information" page.
![](https://main.qcloudimg.com/raw/1e2b43c46dcb77dacbe7fa9cd158dedf.png)



## References
You can also use the `CreateCluster` API to create a cluster. For more information, see [CreateCluster API Documentation](https://intl.cloud.tencent.com/document/product/457/32027).
