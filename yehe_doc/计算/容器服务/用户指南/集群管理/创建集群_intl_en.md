## Scenario
Tencent Cloud TKE provides two methods for cluster creation: [Using a template to create a cluster](#TemplateCreation) and [Creating a custom cluster](#CustomClusterCreation). During cluster creation, TKE also allows users to create or use existing CVMs as the initial nodes of the cluster. This document introduces these two cluster creation methods.


## Operating System Description<span id="OS"></span>

- Changes to the OS only apply to new nodes and reinstalled nodes, but not existing nodes.
- Nodes under the same cluster can use different OS versions, which does not affect cluster features.
- For details on how to change the OS for a cluster, see [Related Operations](#RelatedOperations).
- To use the custom image feature, [submit a ticket](https://console.qcloud.com/workorder/category?level1_id=6&level2_id=350&source=0&data_title=%E5%AE%B9%E5%99%aA8%E6%9C%8D%E5%8A%A1TKE&level3_id=718&radio_title=%E5%AE%B9%E5%99%A8%E9%9B%86%E7%BE%A4%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98&queue=97&scene_code=16798&step=2) to apply for it.
>
>- If you need to use the custom image feature, create custom images based on the basic image provided by TKE.
>- Currently, only modifications within a single OS type are supported. For example, you can use the CentOS basic image to create a CentOS custom image.
>

## Procedure
### Using the template to create a cluster<span id="TemplateCreation"></span>

1. Log in to the [Tencent Cloud TKE console](https://console.cloud.tencent.com/tke2) and click **Clusters** in the left sidebar.
2. On the **Cluster Management** page, click **Template Creation** above the cluster list.
3. The template-based creation feature provides you with multiple templates for creating managed clusters, self-deployed clusters, and elastic clusters. You can choose a template based on your actual requirements.
 - **Managed cluster**: if you create a Kubernetes managed cluster, you do not need to purchase and manage the cluster management node and only need to purchase worker node resources to deploy business applications.
 - **Self-deployed cluster**: if you create a Kubernetes self-deployed cluster, you need to purchase and manage the cluster management and worker nodes. You will hold all the management and operation permissions of the cluster.
 - **Elastic cluster**: if you create a serverless Kubernetes cluster, you do not need to manage any node resources of the cluster and can quickly deploy business applications.
4. This document uses the “Standard Cluster” template under **Managed Cluster** as an example. After choosing **Standard Cluster**, go to the page for creating a cluster. 
> When using a cluster template to create a cluster, all configuration items adopt their default values. You can directly click **Next** or refer to the directions in [Creating a custom image](#CustomClusterCreation) to customize the configuration.
>
5. Click **Finish**.



### Creating a custom cluster<span id="CustomClusterCreation"></span>

#### Entering cluster information

1. <span id="step1">Log in to the [Tencent Cloud TKE console](https://console.cloud.tencent.com/tke2), and click **Clusters** in the left sidebar.</span>
2. On the **Cluster Management** page, click **Create** above the cluster list.
3. On the "Create a cluster" page, set basic cluster information.
 - **Cluster Name**: the name of the cluster to be created, with a length limited to 60 characters.
 - **Project**: select a project based on your actual requirements. Newly added resources will be automatically assigned to this project.
 - **Kubernetes version**: multiple Kubernetes versions are available. For feature comparison between versions, see [Supported Versions of the Kubernetes Documentation](https://kubernetes.io/docs/home/supported-doc-versions/).
 - **Runtime components**: choose **docker** or **containerd**. For details, see [How to Choose Containerd and Docker](https://intl.cloud.tencent.com/document/product/457/31088).
 - **Region**: the region where the cluster will be created. We recommend that you select a region close to your customers to minimize the access latency and improve the download speed.
 - **Cluster Network**: assigns IP addresses that are within the node network address range to CVMs in the cluster. For details, see [Network Settings for Containers and Nodes](https://intl.cloud.tencent.com/document/product/457/9083).
 - **Container Network**: assigns IP addresses that are within the container network address range to containers in the cluster. For details, see [Network Settings for Containers and Nodes](https://intl.cloud.tencent.com/document/product/457/9083).
 - **Operating System**: select an operating system based on your actual requirements.
 - **Cluster Description**: enter information about the cluster, which will be displayed on the **Cluster information** page.
 - **Advanced Settings**: you can set IPVS.
 IPVS applies to scenarios where large-scale services are run on a cluster, and it cannot be disabled once enabled. For details, see [Enabling IPVS for a Cluster](https://intl.cloud.tencent.com/document/product/457/30641).
4. Click **Next**.

#### Selecting a model
In the “Select the model” step, two options: **Add** and **Deploy Later** are provided for **Node Source**. You can choose the option that suits your actual situation. 
 - **Deploy Later**: perform [Create a cluster using an existing CVM](#UseExistingCVMCreateCluster).
 - **Add**: perform [Create a cluster using a new CVM](#NotUseExistingCVMCreateCluster).

<span id="UseExistingCVMCreateCluster"></span>
**Create a cluster using existing CVMs**
>
> - The selected CVM will have the operating system reinstalled, and all data in the system disk will be cleared.
> - The selected CVM will be migrated to the project of the cluster. All related security groups will be unbound. You need to bind them again manually.
>
1. In the “Select the model” step, select a deployment mode and model based on the following information.
 Main parameters include:
- **Master**: the deployment mode of the Master node determines the management mode of your cluster. The **Hosting** and **Independent deployment** cluster management modes are available. For details, see [Cluster Overview](https://intl.cloud.tencent.com/document/product/457/30635). In this document, **Hosting** is used as an example.
   - **Worker Configuration**: select existing CVMs based on actual requirements.
2. Click **Next** to start [configuring a CVM](#ConfigureCVM).

<span id="NotUseExistingCVMCreateCluster"></span>
**Create a cluster using a new CVM**
1. In the “Select the model” step, select a deployment mode and model based on the following information.
 Main parameters include:
- **Master**: the deployment mode of the Master node determines the management mode of your cluster. The **Hosting** and **Independent deployment** cluster management modes are available. For details, see [Cluster Overview](https://intl.cloud.tencent.com/document/product/457/30635). In this document, **Hosting** is used as an example.
  - **Billing Mode**: **pay-as-you-go** is supported. For details, see [Billing Modes](https://intl.cloud.tencent.com/document/product/213/2180).
   - **Worker Configuration**: when **Node Source** is set to **New Node**, the settings under this module are as above by default. You can change them based on your actual requirements.
      - **Availability Zone**: you can select multiple availability zones at the same time to deploy your Master or Etcd nodes to ensure higher availability of the cluster.
      - **Node Network**: you can select multiple subnet resources at the same time to deploy your Master or Etcd nodes to ensure higher availability of the cluster.
      - **Model**: choose a model higher than CPU 4-core. For details, see [Instance Types](https://intl.cloud.tencent.com/document/product/213/11518).
      - **System disk**: the default value is "HDD cloud disk - 50 GB". You can select local disk, HDD cloud disk, SSD cloud disk, or Premium Cloud Storage based on your actual model. For details, see [Overview](https://intl.cloud.tencent.com/document/product/213/4952).
      - **Data disk**: as it is not recommended to deploy other applications in the Master and Etcd nodes, no data disk is configured for them by default. You can purchase one and add it if needed.
      - **Public network bandwidth**: select **Assign free public IP** and the system will assign a public IP address for free. Two billing methods are available. For details, see [Public Network Billing Methods](https://intl.cloud.tencent.com/document/product/213/10578).
      -  **Quantity**: set this parameter based on your actual requirements.
> In independent deployment mode, you can refer to the Worker configuration for the configuration settings of the Masters model. At least three Master models should be deployed. Cross-AZ deployment is supported.
>
2. <span id="step7">Click **Next** to start [configuring a CVM](#ConfigureCVM).</span>

<span id="ConfigureCVM"></span>
#### Configuring a CVM
1. In the “CVM Configuration” step, configure a CVM based on the following information.
 - **Container Directory**: by default, this option is not selected. If it is selected, you can set the container and image storage directory. We recommend that you store containers and images in data disks.
 - **Security Group**: the security group has a firewall feature and is used to set the network access control of the CVM. The following settings are supported:
    - Create and bind the default security group. You can preview the default security group rules.
    - Based on business requirements, you can click **Add Security Group** to configure custom security group rules.
    For details, see [TKE Security Group Settings](https://intl.cloud.tencent.com/document/product/457/9084).
 - **Login Methods**: three login methods are available.
    - **SSH Key Pair**: a key pair is a pair of parameters generated by an algorithm. Compared to regular passwords, it is a more secure way to log in to a CVM. For details, see [SSH Key](https://intl.cloud.tencent.com/document/product/213/6092).
    - **Random Password**: an automatically generated password will be sent to your [Message Center](https://console.cloud.tencent.com/message). 
    - **Custom Password**: set a password as prompted.
2. Click **Next** to check and confirm the configuration information.
3. Click **Finish**.



## Related Operations<span id="RelatedOperations"></span>

### Changing the default OS of a cluster
>
> - Before changing the default OS of a cluster, read [Operating System Description](#OS) carefully to learn about the relevant risks.
> - If you need to perform script configuration on a node, pay attention to adaptation between the script and the OS. We recommend that you verify whether the OS of the node and the script are mutually adapted after you perform script configuration on the node.

1. Log in to the [Tencent Cloud TKE console](https://console.cloud.tencent.com/tke2) and click **Clusters** in the left sidebar.
2. On the **Cluster Management** page, choose **More** -> **Query Cluster Credentials** on the right of the row where the target cluster is located to enter the basic information page of the cluster.
3. In “Node and Network Information”, click <img src="https://main.qcloudimg.com/raw/12834a28b9839ffe9a3723ca23ba19ce.png" style="margin:-3px 0px"> on the right of **Default OS**.
4. In the displayed **Set Cluster OS** window, change the OS and click **Submit**.

