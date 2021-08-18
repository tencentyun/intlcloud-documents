## Overview
Tencent Cloud TKE offers two ways to create clusters: [creating a cluster via template](#TemplateCreation) and [customizing a cluster](#CustomClusterCreation). This document describes how to create clusters and all necessary resources, such as VPCs, subnets, and security groups, using templates and custom configurations.

## Prerequisites

Before creating a cluster, you need to complete the following preparations:
- [Sign up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and complete [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).
- When you log in to the [TKE console](https://console.cloud.tencent.com/tke2) for the first time, you need to grant the current account TKE permissions for operating on CVMs, CLBs, CBS, and other cloud resources. For more information, see [Description of Role Permissions Related to Service Authorization](https://intl.cloud.tencent.com/document/product/457/37808).
- To create a container cluster whose network type is virtual private cloud (VPC), you need to [create a VPC](https://intl.cloud.tencent.com/document/product/215/31805) in the target region and [create a subnet](https://intl.cloud.tencent.com/document/product/215/31806) in the target availability zone under the VPC.
- If you do not use the default security group, you need to [create a security group](https://intl.cloud.tencent.com/document/product/213/34271) in the target region and add a security group rule that meets your business requirements.
- To bind a SSH key pair when creating a Linux instance, you need to [create a SSH key](https://intl.cloud.tencent.com/document/product/213/16691) for the target project.
- When you create a cluster, you will use the resources such as VPCs, subnets, and security groups. Each region has a resource quota. For more information on resource quotas, refer to [Quota Limits for Cluster Purchase](https://intl.cloud.tencent.com/document/product/457/9087).





## Directions

### Creating a cluster via templates[](id:TemplateCreation)

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cluster** in the left sidebar.
2. In the **Cluster Management** page, click **Create with a Template** above the cluster list, as shown below:
![](https://main.qcloudimg.com/raw/22e1a2aa51008198b65c81dd08675019.png)
3. Multiple templates are provided for creating managed clusters, self-deployed clusters, and elastic clusters. You can choose a template based on your actual requirements.
 - **Managed cluster**: if you create a Kubernetes managed cluster, you do not need to purchase and manage the cluster master node and only need to purchase worker node resources to deploy business applications.
 - **Self-deployed cluster**: if you create a self-deployed Kubernetes cluster, you need to purchase and manage the master and worker nodes of the cluster. You will have all the management and operation permissions of the cluster.
 - **Elastic cluster**: if you create a serverless Kubernetes cluster, you do not need to manage any node resources of the cluster and can quickly deploy business applications.
4. This document uses the “Basic Cluster” template under **Managed Cluster** as an example. Select the **Basic Cluster** and go to the **Create Basic Cluster** page.
>?When using a cluster template to create a cluster, all configuration items adopt their default values. You can directly click **Next** or refer to the directions in [customizing a cluster](#CustomClusterCreation) to customize the configuration.
>
5. Click **Done**.



### Customizing a cluster[](id:CustomClusterCreation)

#### Entering cluster information

1. [](id:step1)Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Clusters** in the left sidebar.
2. On the "Cluster Management" page, click **Create** above the cluster list.
3. On **Create Cluster** page, configure the basic information of the cluster as shown in the figure below:
![](https://main.qcloudimg.com/raw/31e3fa0551850812cacef99fd6d75cf9.png)
 - **Cluster Name**: the name of the cluster to be created, with a length up to 60 characters.
 - **Project of New-added Resource**: select a project as needed. The newly added resources will be automatically assigned to this project.
 - **Kubernetes Version**: multiple Kubernetes versions are available. For feature comparison between different versions, see [Supported Versions of the Kubernetes Documentation](https://kubernetes.io/docs/home/supported-doc-versions/).
 - **Runtime Component**: choose **docker** or **containerd**. For details, see [How to Choose Containerd and Docker](https://intl.cloud.tencent.com/document/product/457/31088).
 - **Region**: the region where the cluster will be created. We recommend that you select a region close to your customers to minimize the access latency and improve the download speed.
 - **Cluster Network**: assigns IP addresses that are within the node IP range to CVMs in the cluster. For details, see [Network Settings for Containers and Nodes](https://intl.cloud.tencent.com/document/product/457/9083).
 - **Container Network Add-on**: **Global Router** and **VPC-CNI** network modes are provided. For more information, see [How to Choose TKE Network Mode](https://intl.cloud.tencent.com/document/product/457/38966).
 - **Container Network**: assigns IP addresses that are within the container network address range to containers in the cluster. For details, see [Network Settings for Containers and Nodes](https://intl.cloud.tencent.com/document/product/457/9083).
 - **Operating System**: select an operating system based on your actual requirements.
 - **Cluster Description**: enter information about the cluster, which will be displayed on the **Cluster information** page.
 - **Advanced Settings** (optional):
    - **Tencent Cloud Tags**: after binding tags to the cluster, you can categorize the resources. For more information, see [Querying Resources by Tag](https://intl.cloud.tencent.com/document/product/651/32582).   
    - **Deletion Protection**: when it's enabled, the cluster will not be deleted by mis-operation on console or by API.
    - **Kube-proxy Proxy Mode**: select iptables or ipvs. IPVS mode is applicable to large-scale services. You cannot disable it once it is enabled. For details, refer to [Enabling IPVS for a Cluster](https://intl.cloud.tencent.com/document/product/457/30641).
    - **Custom Parameters**: specify the custom parameters to configure the cluster.
    - **Runtime Version**: select the version of the container runtime component.
4. Click **Next**.

#### Selecting a Model
1. In **Select Model** page, confirm the billing mode, select an availability zone and the corresponding subnet, and confirm the node model, as shown below:
![](https://main.qcloudimg.com/raw/3e005a89586fd9113755aa82975bf55f.png)
  - **Node Source**: there are two options: **Add node** and **Existing nodes**.
<dx-tabs>
::: Adding a node
Create a cluster by adding nodes (that is, by adding CVMs). The details are as follows:

In the **Select Model** step, select a deployment mode and model based on the following information, as shown below:
![](https://main.qcloudimg.com/raw/027ff16d127413aea2b32dde9ba28e7b.png)
 The main parameters are described as follows:

   - **Master Node**: the deployment mode of the Master node determines the management mode of your cluster. The **Managed** and **Self-deployed** cluster management modes are available. For details, see [Cluster Overview](https://intl.cloud.tencent.com/document/product/457/30635). In this document, **Managed** is used as an example.
  - **Billing Mode**: **pay-as-you-go** is supported. For details, see [Billing Plans](https://intl.cloud.tencent.com/document/product/213/2180).
   - **Worker Configurations**: when **Node Source** is set to **Add Node**, the settings under this module are as above by default. You can change them based on your actual requirements.
      - **Availability Zone**: you can select multiple availability zones at the same time to deploy your Master or Etcd nodes to ensure higher availability of the cluster.
      - **Node Network**: you can select multiple subnet resources at the same time to deploy your Master or Etcd nodes to ensure higher availability of the cluster.
      - **Model**: choose a model higher than CPU 4-core. For details, see [Instance Types](https://intl.cloud.tencent.com/document/product/213/11518).
      - **System disk**: the default value is **HDD cloud disk - 50 GB**. You can select local disk, HDD cloud disk, SSD cloud disk, or premium cloud disk based on your actual model. For details, see [Storage Overview](https://intl.cloud.tencent.com/document/product/213/4952).
      - **Data disk**: as it is not recommended to deploy other applications in the Master and Etcd nodes, no data disk is configured for them by default. You can purchase one and add it if needed.
      - **Public network bandwidth**: select **Assign free public IP** and the system will assign a public IP address for free. Two billing methods are available. For details, see [Public Network Billing](https://intl.cloud.tencent.com/document/product/213/10578).
      - **Node Name**: the name of the computer in the OS (the node name displayed by running the `kubectl get nodes` command`). It is a cluster attribute. The node name can be named in the following two modes:
        - **Auto-generated**: the node name defaults to the private IP of the node.
        - **Custom Name**: you can use sequential numbering or custom format string. It can contains 2-60 characters, including lower-case letters, numbers, hyphens ("-") and periods ("."). Symbols cannot be placed at the beginning nor end, and cannot be used consecutively. For more naming rules, see [Batch Sequential Naming or Pattern String-Based Naming](https://intl.cloud.tencent.com/document/product/213/32020).
  >!Due to the naming restriction of kubernetes node, you can only use the lower-case letters when customizing the node name, for example, 'cvm {R:13}-big{R:2}-test'.
  >
        - **Instance Name**: the CVM instance name displayed in the console, which is determined by the naming mode of host name.
         - When the node name is automatically generated, it supports sequential numbering or custom format for multiple instances. Up to 60 characters allowed. The instance name is automatically generated by default in the format of `tke_cluster id_worker`.
         - When the node name is customized, the instance name is the same as the hostname without reconfiguration.
      - **Amount**: set the number of instances as needed.
>?In the self-deployed mode, you can refer to the Worker configuration for the configuration settings of the Masters model. At least three Master models should be deployed. Cross-AZ deployment is supported.
>

:::
::: Existing nodes [](id:UseExistingCVMCreateCluster)
Create a cluster using the existing nodes (that is, by using the existing CVMs). The details are as follows:

>!
> - The selected CVMs will be reinstalled and all data in the system disk will be cleared.
> - The selected CVMs will be migrated to the project of the cluster. All related security groups will be unbound. You need to bind them manually again.
>- If you set the data disk mounting parameters when configuring the CVM, this parameter will be applied to **all Master and Worker nodes**. For more information, see the **Data Disk Settings** in [Adding an existing node](https://intl.cloud.tencent.com/document/product/457/30652).
>

 In the **Select Model** step, select a deployment mode and model based on the following information, as shown below:
![](https://main.qcloudimg.com/raw/883f0d559eba35b034c36423ec45f2f9.png)
 The main parameters are described as follows:

   - **Master Node**: the deployment mode of the Master node determines the management mode of your cluster. The **Managed** and **Self-deployed** cluster management modes are available. For details, see [Cluster Overview](https://intl.cloud.tencent.com/document/product/457/30635). In this document, **Managed** is used as an example.
   - **Worker Configurations**: select the existing CVMs based on actual needs.

:::
</dx-tabs>
2. Click **Next** to start [configuring a CVM](#ConfigureCVM).

[](id:ConfigureCVM)
#### CVM configuration
1. In the “CVM Configuration” step, configure a CVM based on the following information, as shown below:
![](https://main.qcloudimg.com/raw/24a166447e301672141a4f2257d7a206.png)
 - **Container Directory**: check this option to set up the container and image storage directory. We recommend that you store to the data disk, such as `/var/lib/docker`.
 - **Security Group**: the security group works as a firewall to control network access of the CVM. The following settings are supported:
    - Create and bind the default security group. You can preview the default security group rules.
    - Add security group to configure custom security group rules according to your actual needs.
    For details, see [TKE Security Group Settings](https://intl.cloud.tencent.com/document/product/457/9084).
 - **Login Method**: three login methods are available.
    - **SSH Key Pair**: a key pair is a pair of parameters generated by an algorithm. Compared to regular passwords, it is a more secure way to log in to a CVM. For details, see [SSH Key](https://intl.cloud.tencent.com/document/product/213/6092).
    - **Random Password**: the system sends an automatically generated password to your [Message Center](https://console.cloud.tencent.com/message). 
    - **Custom Password**: set a password as prompted.
  - **Security Services**: free DDoS Protection, Web Application Firewall (WAF), and Cloud Workload Protection are activated by default. For more information, see [Cloud Workload Protection](https://intl.cloud.tencent.com/product/cwp).
  - **Cloud Monitor**: free monitoring, analysis, and alarms are activated by default, and components are installed to obtain CVM monitoring metrics. For more information, see [Cloud Monitor](https://intl.cloud.tencent.com/product/cm).
2. (Optional) Click **Advanced Settings** to view or configure more information, as shown in the following figure.
![](https://main.qcloudimg.com/raw/f6bd03236aac6a6c56557dced60fda02.png)
 - **CAM Role**: you can bind all the nodes created this time to the same CAM role, and grant the authorization policy bound to the role to the nodes. For more information, see [Managing Roles](https://intl.cloud.tencent.com/document/product/213/38290).
 - **Node Launch Configuration**: specify custom data to configure node, that is, to run the configured script when the node is started up. You need to ensure the reentrant and retry logic of the script. The script and its log files can be viewed at the node path: `/usr/local/qcloud/tke/userscript`.
 - **Cordon**: after you check **Cordon this node**, new Pods cannot be scheduled to this node. You can uncordon the node manually, or execute the [uncordon command](https://intl.cloud.tencent.com/document/product/457/30654) in custom data as needed.
  - **Label**: click **Add** to customize the label. The label set here will be automatically added to the initial nodes of the cluster, and is used to filter and manage nodes in the future.
3. Click **Next** to configure the component.




#### Component configurations
1. In the **Component Configurations** step, configure a component based on the following information, as shown below:
![](https://main.qcloudimg.com/raw/5d7dc6f9da2bcc56961eda8d3cfc4a68.png)
 - **Addon**: you can select the add-ons such as storage, monitor, and image as needed. For more information, see [Add-on Overview](https://intl.cloud.tencent.com/document/product/457/33988).
 - **Log Service**: the cluster auditing is enabled by default. For more information, see [Cluster Audit](https://intl.cloud.tencent.com/document/product/457/38338).
2. Click **Next** to check and confirm the configuration information.


#### Information confirmation
In the “Confirm Info” page, confirm the selected configuration information and billing mode for the cluster and click **Done**.


### Viewing the cluster
You can view clusters that have been created in the [cluster list](https://console.cloud.tencent.com/tke2/cluster?rid=1). You can click the cluster ID to enter the details page, and then view the cluster, node, and network information on the “Basic Information” page, as shown below:
![](https://main.qcloudimg.com/raw/1e2b43c46dcb77dacbe7fa9cd158dedf.png)



## Reference
You can also use the `CreateCluster` API to create a cluster. For more information, see [CreateCluster API Documentation](https://intl.cloud.tencent.com/document/product/457/32027).
