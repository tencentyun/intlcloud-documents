## Introduction
Tencent Cloud TKE offers two ways to create clusters: [Creating Clusters Using Templates](#TemplateCreation] and [Creating Clusters Using Custom Configurations](#CustomClusterCreation). This document describes how to create clusters and all necessary resources, such as VPCs, subnets, and security groups, using templates and custom configurations.

## Prerequisites
TKE uses cloud resources such as CVM instances, CLB instances, and CBS cloud disks. If you are using TKE for the first time, make sure you have the appropriate service authorization so that you can use these cloud resources. TKE also uses VPCs, subnets, and security groups. Each region has a resource quota. For more information on resource quotas, see [Quota Limits for Cluster Purchase](https://intl.cloud.tencent.com/document/product/457/9087).

>? If this is not the first time you are creating a TKE cluster, skip to [Operating Systems](#OS) for notes on operating systems.
>
If you are creating a TKE cluster for the first time, go to [Related Operations](#RelatedOperations) to create the necessary resources for the cluster. The following is a list of all the resources you need to create:
- [Identity Verification](#Verified)
- [Service Authorization](#ServiceAuthorization)
- [VPCs](#PVC)
- [Subnets](#Subnet)
- [Security Groups](#NewSecurityGroup)
- [SSH Keys](#SSH)

<span id="OS"></span>
## Notes on the OS

- Changes to the OS only affect new nodes and reinstalled nodes, and do not affect existing nodes.
- Nodes in the same cluster can use different OS versions without affecting cluster functionality.
- One script does not suit all OSs. After configuring a node with a script, run a test to make sure it is compatible with the OS.
- For more information on how to change the OS for a cluster, see [Related Operations](#RelatedOperations).
- To use the custom image feature, please apply by [submitting a ticket](https://console.qcloud.com/workorder/category?level1_id=6&level2_id=350&source=0&data_title=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1TKE&level3_id=718&radio_title=%E5%AE%B9%E5%99%A8%E9%9B%86%E7%BE%A4%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98&queue=97&scene_code=16798&step=2).
>!
>- If you need to use the custom image feature, create custom images based on the basic image provided by TKE.
>- Currently, only modifications within a single OS type are supported. For example, you can use the CentOS basic image to create a CentOS custom image.
>


## Directions
<span id="TemplateCreation"></span>

### Creating clusters using templates

1. Log in to the [Tencent Cloud TKE console](https://console.cloud.tencent.com/tke2) and click **Clusters** in the left sidebar.
2. Click **Template Creation** above the list of clusters on the **Cluster Management** page, as shown in the figure below:
![](https://main.qcloudimg.com/raw/22e1a2aa51008198b65c81dd08675019.png)
3. The template-based creation feature provides you with multiple templates for creating managed clusters, self-deployed clusters, and elastic clusters. You can choose a template based on your actual requirements.
 - **Managed cluster**: if you create a Kubernetes managed cluster, you do not need to purchase and manage the cluster master node and only need to purchase worker node resources to deploy business applications.
 - **Self-deployed cluster**: if you create a self-deployed Kubernetes cluster, you need to purchase and manage the master and worker nodes of the cluster. You will have all the management and operation permissions of the cluster.
 - **Elastic cluster**: if you create a serverless Kubernetes cluster, you do not need to manage any node resources of the cluster and can quickly deploy business applications.
4. This document uses the “Standard Cluster” template under **Managed Cluster** as an example. After choosing **Standard Cluster**, go to the page for creating a cluster.
>? When using a cluster template to create a cluster, all configuration items adopt their default values. You can directly click **Next** or refer to the directions in [Creating a custom image](#CustomClusterCreation) to customize the configuration.
>
5. Click **Finish**.


<span id="CustomClusterCreation"></span>
### Creating a custom image

#### Entering cluster information

1. <span id="step1">Log in to the [Tencent Cloud TKE console](https://console.cloud.tencent.com/tke2), and click **Clusters** in the left sidebar.</span>
2. On the **Cluster Management** page, click **Create** above the cluster list.
3. On the **Create a Cluster** page, configure the basic information of the cluster, as shown in the figure below:
![](https://main.qcloudimg.com/raw/6467323de4e42c4cc74c7a235cac2265.png)
 - **Cluster Name**: the name of the cluster to be created, with a length up to 60 characters.
 - **Project of New-added Resource**: select the project based on actual needs. Newly added resources will be automatically assigned to this project.
 - **Kubernetes Version**: multiple Kubernetes versions are available. For feature comparison between different versions, see [Supported Versions of the Kubernetes Documentation](https://kubernetes.io/docs/home/supported-doc-versions/).
 - **Runtime Component**: choose **docker** or **containerd**. For more information, see [How to Choose Containerd and Docker](https://intl.cloud.tencent.com/document/product/457/31088).
 - **Region**: the region where the cluster to be created is located. We recommend that you select the region closest to you to help minimize access latency and improve the download speed.
 - **Cluster Network**: assigns IP addresses that are within the node IP range to CVMs in the cluster. 
 - **Container Network**: assigns IP addresses that are within the container network address range to containers in the cluster.
 - **Operating System**: select the OS based on your requirements.
 - **Cluster Description**: enter the information about the cluster, which will be displayed on the **Cluster Information** page.
 - **Advanced Settings**: you can set IPVS.
 IPVS is useful for large-scale services. You cannot disable it once it is enabled. For more information, see [Enabling IPVS for a Cluster](https://intl.cloud.tencent.com/document/product/457/30641).
4. Click **Next**.

#### Selecting a model
In the **Select the model** step, you can choose **Existing nodes** or **Add**. 
 - **Existing nodes**: [Create a cluster using existing CVMs](#UseExistingCVMCreateCluster).
 - **Add**: [Create a cluster using a new CVM](#NotUseExistingCVMCreateCluster).

<span id="UseExistingCVMCreateCluster"></span>
**Create a cluster using existing CVMs**
>!
> - The selected CVM will have the operating system reinstalled, and all data in the system disk will be cleared.
> - The selected CVM will be migrated to the project of the cluster. All related security groups will be unbound. You need to bind them again manually.
>
1. In the **Select the model** step, select a deployment mode and model based on the following information.
![](https://main.qcloudimg.com/raw/883f0d559eba35b034c36423ec45f2f9.png)
 Main parameters include:
   - **Master**: the deployment mode of the master node determines the management mode of your cluster. The **Hosting** and **Independent deployment** cluster management modes are available. For more information, see [Cluster Overview](https://intl.cloud.tencent.com/document/product/457/30635). In this document, **Hosting** is used as an example.
   - **Worker Configuration**: select existing CVMs based on actual requirements.
2. Click **Next** to start [configuring a CVM](#ConfigureCVM).

<span id="NotUseExistingCVMCreateCluster"></span>
**Create a cluster using a new CVM**
1. In the **Select the model** step, select a deployment mode and model based on the following information.
![](https://main.qcloudimg.com/raw/ffe511e82ff82111ce565be20ee1af85.png)
 Main parameters include:
   - **Master**: the deployment mode of the master node determines the management mode of your cluster. The **Hosting** and **Independent deployment** cluster management modes are available. For more information, see [Cluster Overview](https://intl.cloud.tencent.com/document/product/457/30635). In this document, **Hosting** is used as an example.
  - **Billing Mode**: **pay-as-you-go** is supported. For more information, see [Billing Modes](https://intl.cloud.tencent.com/document/product/213/2180).
   - **Worker Configuration**: when **Node Source** is set to **New Node**, the settings under this module are as above by default. You can change them based on your actual requirements.
      - **Availability Zone**: you can select multiple availability zones at the same time to deploy your Master or Etcd nodes to ensure higher availability of the cluster.
      - **Node Network**: you can select multiple subnet resources at the same time to deploy your Master or Etcd nodes to ensure higher availability of the cluster.
      - **Model**: choose a model higher than CPU 4-core. For more information, see [Instance Types](https://intl.cloud.tencent.com/document/product/213/11518).
      - **System disk**: the default value is **HDD cloud disk - 50 GB**. You can select local disk, HDD cloud disk, SSD cloud disk, or Premium Cloud Storage based on your actual model. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/213/4952).
      - **Data disk**: as it is not recommended to deploy other applications in the Master and Etcd nodes, no data disk is configured for them by default. You can purchase one and add it if needed.
      - **Public network bandwidth**: select **Assign free public IP** and the system will assign a public IP address for free. Two billing methods are available. For more information, see [Public Network Billing Methods](https://intl.cloud.tencent.com/document/product/213/10578).
      -  **Quantity**: set this parameter based on your actual requirements.
>! In independent deployment mode, you can refer to the Worker configuration for the configuration settings of the Masters model. At least three Master models should be deployed. Cross-AZ deployment is supported.
>
2. <span id="step7">Click **Next** to start [configuring a CVM](#ConfigureCVM).</span>

<span id="ConfigureCVM"></span>
#### Configuring a CVM
1. In the “CVM Configuration” step, configure a CVM based on the following information.
![](https://main.qcloudimg.com/raw/e778a2a91d274c3ae9f0b186e5a9dbd3.png)
 - **Container Directory**: by default, this option is not selected. If it is selected, you can set the container and image storage directory. We recommend that you store containers and images in data disks.
 - **Security Group**: the security group works as a firewall to control the network access of the CVM. The following settings are supported:
    - Create and bind the default security group. You can preview the default security group rules.
    - Click **Add Security Group** to configure custom security group rules according to your actual requirements.
    For more information, see [TKE Security Group Settings](https://intl.cloud.tencent.com/document/product/457/9084).
 - **Login Methods**: three login methods are available.
    - **SSH Key Pair**: a key pair is a pair of parameters generated by an algorithm. It is a way to log in to a CVM instance that is more secure than regular passwords. For more information, see [SSH Key](https://intl.cloud.tencent.com/document/product/213/6092).
    - **Random Password**: the system sends an automatically generated password to you via an [Internal Message](https://console.cloud.tencent.com/message). 
    - **Custom Password**: set a corresponding password as prompted.
2. Click **Next** to check and confirm the configuration information.
3. Click **Finish**.
<span id="RelatedOperations"></span>
## Relevant Operations
<span id="Verified"></span>
### Identity verification

#### Verification entry
Log in to the [Tencent Cloud console](https://console.cloud.tencent.com/). On the **Overview** page, click **Complete Identity Verification** to go to the identity verification page, as shown in the figure below:
![](https://main.qcloudimg.com/raw/efc81878de5040a7ed50b2e5f9ab28e6.png)

#### Verification steps
1. On the **Select Verification Type** page, select **Start Individual Verification** or **Start Enterprise Verification** based on your requirements, and complete verification according to the following information.
- **Individual Verification**: after the Tencent Cloud account passes individual identity verification, this account and its cloud resources belong to you and can be used for individual operation events on the official website of Tencent Cloud. However, it cannot be used for enterprise operation events or used to apply for VAT special invoices.
- **Enterprise Verification**: after the Tencent Cloud account passes enterprise identity verification, this account and its cloud resources belong to you and can be used for enterprise operation events on the official website of Tencent Cloud. It can be used to apply for VAT special invoices, but cannot be used for individual operation events.
2. After verification is completed, you can use this Tencent Cloud account to create clusters and perform other operations.
<span id="ServiceAuthorization"></span>

### Service authorization

1. When you log in to the [Tencent Cloud TKE console](https://console.cloud.tencent.com/tke2) for the first time, click **Clusters** in the left sidebar. The **Service authorization** page appears.
2. Click **Go to access management** to go to the **Role management** page, as shown in the figure below.
![](https://main.qcloudimg.com/raw/c1eac9f12a89e099badda5f799e11c52.png)
3. Click **Grant authorization** and complete identity verification.

<span id="PVC"></span>

### Creating a VPC

1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1). Select a region at the top of the VPC list and click **+Create**, as shown in the figure below.
![](https://main.qcloudimg.com/raw/2075937aca988b69f9ff1c15c5b31b20.png)
2. On the **Create VPC** page, set the basic information of the VPC, as shown in the figure below.
![](https://main.qcloudimg.com/raw/a5a841b9504a7bd842a005503749f670.png)
 - **VPC information**    
	- **Region**: the region of the VPC.
	- **Name**: the name of the VPC.
	- **IPv4 CIDR Block**: the VPC IPv4 CIDR block. You can use one of the following CIDR blocks. **They cannot be modified after creation**.**If you have multiple VPCs and they need to communicate with one another, make sure their CIDR blocks do not overlap**.
		- `10.0.0.0` - `10.255.255.255` (mask range: 16 to 28)
		- `172.16.0.0` - `172.31.255.255` (mask range: 16 to 28)
		- `192.168.0.0` - `192.168.255.255` (mask range: 16 to 28)
 - **Original subnet information**
	- **Subnet name**: the name of the subnet.
	- **IPv4 CIDR Block**: the subnet IPv4 CIDR block. **They cannot be modified after creation**. The subnet CIDR block must be the same as or a subset of the VPC CIDR block. For example, if the VPC CIDR block is `192.168.0.0/16`, the subnet CIDR block can be `192.168.0.0/16` or `192.168.0.0/17`.
	- **Availability Zone**: select a desired availability zone.
	- **Associated route table**: a subnet must be associated with a route table for traffic forwarding. The console provides a **Default** route table.
3. Click **OK** to create a VPC.
<span id="Subnet"></span>
### Creating a subnet

1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1) and click **Subnet** in the left sidebar.
2. On the **Subnet** page, click **+Create**. The **Create a Subnet** page appears, where you can configure the Subnet Name, VPC IP Range, CIDR Block, Availability Zone, and associated route table, as shown in the figure below.
![](https://main.qcloudimg.com/raw/f50bb23310ef463253dcbf8c2e503adb.png)
3. (Optional) Click **+New Line** to create multiple subnets at a time.
4. Click **Create**.
<span id="NewSecurityGroup"></span>
### Creating a security group
You can create a security group and bind it to a cluster during the cluster creation process, or create a custom security group based on your service requirements and bind it to a cluster. The directions for creating a custom security group are as follows:
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index). Click **Security Group** in the left sidebar to go to the **Security Group** page.
2. Select a region at the top of the page and click **+Create** to go to the **Create a security group** page, as shown in the figure below.
![](https://main.qcloudimg.com/raw/ad4cf4b6c5344bb162fb1acb23370afb.png)
 - **Template**: select a template that suits your needs to simplify the configuration of the security group rules, a shown in the table below.
<table>
	<tr><th>Template</th><th>Description</th><th>Scenario</th></tr>
	<tr><td>Open all ports</td><td>All ports are open to the public and private networks by default, which may security issues.</td><td>-</td></tr>
	<tr><td>Open ports 22，80，443，3389 and ICMP protocol</td><td>Ports 22, 80, 443 and 3389, and the ICMP protocol are open by default. All ports are open to private networks.</td><td>Suitable for instances with web services.</td></tr>
	<tr><td>Custom</td><td>Add rules for the security group you created. For more information on how to add security group rules, see <a href="https://intl.cloud.tencent.com/document/product/213/34272">Adding Security Group Rules</a>.</td><td>-</rd></tr>
</table>
 - **Name**: the name of the security group.
 - **Project**: by default, **Default project** is selected. Select a project to facilitate management.
 - **Notes**: a short description of the security group.
 - **Display template rule**: click to reveal existing security group inbound and outbound rules.
3. Click **OK** to create the security group.
If you select **Custom** as the template for your security group, click **Add rules now** to [add security group rules](https://intl.cloud.tencent.com/document/product/213/34272).

<span id="SSH"></span>
### Creating SSH keys

 1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/) and click [**SSH Key**](https://console.cloud.tencent.com/cvm/sshkey) in the left sidebar to go to the **SSH Key** page.
 2. On the SSH key management page, click **Create a key**.
 3. On the **Create SSH Key** page that appears, configure the SSH key, as shown in the figure below.
![](https://main.qcloudimg.com/raw/55c8e18cc210802077c138b905e24971.png)
  - **Mode**: you can **Create a new key pair** or **Use an existing public key**.
    - If you select **Create a new key pair**, enter a name.
    - If you select **Use an existing public key**, enter the key name and the original public key information.

>! The following is a sample public key:
>```
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCdv1zOdTqtt70iqgCBT6mYbwCP3ASSl6Qidr/LmBkMCbWvSB1PDcZhcVmnkM1Fcltz25UroRmusF6s45HOgU2qZtC4J1jPV1SG6ashUJgJw9TSmnHPvy76BcRFe4xwA75CVfozSqeJejLnHP1oF8Dj+cM7/DLmxbOpJO1kaIx2bVuqYrwQGah6L3nozKSTY9qZ6pBar8TJFmgp4YDaxso78oqBtt0Q82c9MWTMszt3VvfNscS2WY6PFF3OHOlwkUesfPez5OnUeeCFpD3T5UCfTY0yrjbcYqx4WHElZ92RtSNDTbonAxUPHVYi8r6tkVNznBJJ2E+6TphvGIR2wzPl skey-qswnaltn
>```

 4. Click **OK** to go to the *SSH Key Pair Created** page. Click **Download** to save a copy of the private key.
>! Tencent Cloud does not save your private key information. Download and obtain the private key within 10 minutes.


### Changing the default OS of a cluster
>
>? Before changing the default OS of a cluster, read [Operating System Description](#OS) carefully to learn about the relevant risks.

1. Log in to the [Tencent Cloud TKE console](https://console.cloud.tencent.com/tke2) and click **Clusters** in the left sidebar.
2. On the **Cluster Management** page, select **More** -> **Query Cluster Credentials** for the target cluster to go to the basic information page of the cluster.
3. In **Node and Network Information**, click <img src="https://main.qcloudimg.com/raw/12834a28b9839ffe9a3723ca23ba19ce.png" style="margin:-3px 0px"> on the right of **Default OS**, as show in the figure below.
![](https://main.qcloudimg.com/raw/60ada0dd3689faf95ff37bd7c8f8530e.png)
4. On the **Set Cluster OS** page, change the OS and click **Submit**, as shown in the figure below.
![](https://main.qcloudimg.com/raw/da9b11bedb636736016c2fa90b2ec90e.png)

