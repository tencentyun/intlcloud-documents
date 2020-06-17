## Introduction
Tencent Cloud TKE offers two ways to create clusters: [Creating Clusters Using Templates](#TemplateCreation] and [Creating Clusters Using Custom Configurations](#CustomClusterCreation). This article describes how to create clusters and all necessary resources, such as VPCs, subnets, and security groups, using templates and custom configurations.

## Prerequisites
TKE uses cloud resources such as CVM instances, CLB instances, and CBS cloud disks. If you are using TKE for the first time, make sure you have the appropriate service authorization so you can use these cloud resources. TKE also uses VPCs, subnets, and security groups. Each region has a resource quota. For more information on resource quotas, refer to [Quota Limits for Cluster Purchase](https://intl.cloud.tencent.com/document/product/457/9087).

> If this is not the first time you are creating a TKE cluster, skip to [Operating Systems] for notes on operating systems.
>
If you are creating a TKE cluster for the first time, go to [Related Operations] to create the necessary resources for the cluster. The following is a list of all the resources you need to create:
- [Service authorization](#ServiceAuthorization)
- [VPCs](#PVC)
- [Subnets](#Subnet)
- [Security Groups](#NewSecurityGroup)
- [SSH Keys](#SSH)


## Operating Systems<span id="OS"></span>

- Changes to the OS only affect new nodes and reinstalled nodes, not existing nodes.
- Nodes in the same cluster can use different OS versions without affecting cluster functionality.
- One script does not suit all operating systems. After configuring a node with a script, run a test to make sure it is compatible with the operating system.
- For details on how to change the OS for a cluster, refer to [Related Operations](#RelatedOperations).
- If you want to use custom images, [submit a ticket](https://console.qcloud.com/workorder/category?level1_id=6&level2_id=350&source=0&data_title=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1TKE&level3_id=718&radio_title=%E5%AE%B9%E5%99%A8%E9%9B%86%E7%BE%A4%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98&queue=97&scene_code=16798&step=2) for further assistance.
>
>- If you need custom images, use the basic images provided by TKE as starting points.
>- You can only modify basic images to create custom images of the same operating system. For example, you can use CentOS basic images to create custom CentOS images.
>


## Directions
<span id="TemplateCreation"></span>
### Creating clusters using templates

1. Log in to the [Tencent Cloud TKE console](https://console.cloud.tencent.com/tke2) and click **Clusters** in the left sidebar.
2. In the **Cluster Management** page, click **Template Creation** above the cluster list.

3. You can use templates to create managed clusters, self-deployed clusters, and elastic clusters. Choose a template that suits you.
 - **Managed cluster**: if you create a managed cluster, you do not need to purchase and manage the cluster master node. Just purchase worker node resources and you are good to go.
 - **Self-deployed cluster**: if you create a self-deployed cluster, you need to purchase and manage the master and worker nodes of the cluster. You have all the management and operation permissions.
 - **Elastic cluster**: if you create a serverless cluster, you do not need to manage any node resources. Just deploy your applications after purchasing.
4. This article uses the “General Cluster” template under **Managed Cluster** as an example. Select **General Cluster** to go the first step of creating a cluster. 
> The cluster template defines a default value for each configuration item. You can create a cluster using these default values by clicking **Next**, or use [Creating custom clusters](#CustomClusterCreation) as a reference to customize the configuration items.
>
5. Click **Finish**.


<span id="CustomClusterCreation"></span>
### Creating custom clusters

#### Entering cluster information

1. <span id="step1">Log in to the [Tencent Cloud TKE console](https://console.cloud.tencent.com/tke2), and click **Clusters** in the left sidebar.</span>
2. In the **Cluster Management** page, click **Create** above the cluster list.
3. In the **Create a cluster** page, enter the following information:
 - **Cluster Name**: name of the cluster with a limit of 60 characters.
 - **Project of New-added Resource**: select a project to which new resources are automatically assigned.
 - **Kubernetes version**: multiple Kubernetes versions are available. For feature comparison between different versions, refer to [Supported Versions of the Kubernetes Documentation](https://kubernetes.io/docs/home/supported-doc-versions/).
 - **Runtime Component**: select **docker** or **containerd**. For details, refer to [How to Choose Between Containerd and Docker](https://intl.cloud.tencent.com/document/product/457/31088).
 - **Region**: the region where the cluster is located. We recommend that you select the region closest to you to help minimize access latency and improve download speed.
 - **Cluster network**: assigns IP addresses within the node IP range to CVMs instances in the cluster. For details, refer to [Network Settings for Containers and Nodes](https://intl.cloud.tencent.com/document/product/457/9083).
 - **Container Network**: assigns IP addresses within the container network IP range to containers in the cluster. For details, refer to [Network Settings for Containers and Nodes](https://intl.cloud.tencent.com/document/product/457/9083).
 - **Operating system**: select an operating system.
 - **Cluster Description**: Enter the information about the cluster, which will be displayed on the **Cluster information** page.
 - **Advanced Settings**: you can select to enable IPVS.
 IPVS is useful for large-scale services. You cannot disabled it once it is enabled. For details, refer to [Enabling IPVS for a Cluster](https://intl.cloud.tencent.com/document/product/457/30641).
4. Click **Next**.

#### Selecting a model
In the **Select the model** page, select **Existing nodes** or **Add node**. 
 - **Existing nodes**: follow the instructions in [Create a cluster using existing CVM instances](#UseExistingCVMCreateCluster).
 - **Add node**: follow the instructions in [Create a cluster using a new CVM instance](#NotUseExistingCVMCreateCluster).

<span id="UseExistingCVMCreateCluster"></span>
**Create a cluster using existing CVM instances**
>
> - The selected CVM instances will have their operating systems reinstalled, which deletes all data on the system disks.
> - The selected CVM instances will be migrated to the project of the cluster. All associated security groups will be unbound. You need to bind them again manually.
>
1. In the **Select the model** step, select a deployment mode and model based on the following information.
 Main parameters include:
- **Master Node**: how you want your Master node to deploy determines the management mode of your cluster. Options include **Managed** and **Self-deployed**. For details, refer to [Cluster Overview](https://intl.cloud.tencent.com/document/product/457/30635). For the purpose of this article, select **Managed**.
   - **Worker Configurations**: select existing CVM instances that suit your needs.
2. Click **Next** to start [configuring CVM instances](#ConfigureCVM).

<span id="NotUseExistingCVMCreateCluster"></span>
**Create a cluster using new CVM instances**
1. In the **Select the model** step, select a deployment mode and model based on the following information.

 Main parameters include:

   - **Master Node**: how you want your Master node to deploy determines the management mode of your cluster. Options include **Managed** and **Self-deployed**. For details, refer to [Cluster Overview](https://intl.cloud.tencent.com/document/product/457/30635). For the purpose of this article, select **Managed**.
  - **Billing Mode**: **pay-as-you-go** is the only option. For details, refer to [Billing Modes](https://intl.cloud.tencent.com/document/product/213/2180).
   - **Worker Configurations**: if you selected **Add node** for **Node Source**, the default settings are shown in the preceding figure. 
      - **Availability Zone**: you can select multiple availability zones at the same time to deploy your Master or Etcd nodes to ensure higher availability of the cluster.
      - **Node Network**: you can select multiple subnet resources at the same time to deploy your Master or Etcd nodes to ensure higher availability of the cluster.
      - **Model**: choose a model with more than four CPU cores. For details, refer to [Instance Types](https://intl.cloud.tencent.com/document/product/213/11518).
      - **System disk**: the default value is **HDD cloud disk - 50 GB**. Options include local disk, HDD cloud disk, SSD cloud disk, and Premium Cloud Storage. Select one for your model. For details, refer to [Overview](https://intl.cloud.tencent.com/document/product/213/4952).
      - **Data disk**: we recommend you do not deploy other applications on the Master and Etcd nodes. Therefore, no data disk is configured for them by default. You can purchase one and add it if needed.
      - **Public network bandwidth**: select **Assign free public IP** and the system will assign a public IP address for free. Two billing plans are available. For details, refer to [Public Network Billing Plans](https://intl.cloud.tencent.com/document/product/213/10578).
      -  **Quantity**: set this to the number of nodes you want to purchase.
> For Self-deployed clusters, you can refer to the Worker configurations for the configuration settings of the Masters model. At least three Master models should be deployed and you can deploy them across availability zones.
>
2. <span id="step7">Click **Next** to start [CVM Configuration](#ConfigureCVM).</span>

<span id="ConfigureCVM"></span>
#### CVM Configuration
1. In the **CVM Configuration** page, configure the following parameters:
 - **Container Directory**: by default, this option is not selected. Select it to set the container and image storage directory. We recommend that you store containers and images in data disks.
 - **Security Group**: security groups can act as firewalls. You can use them to control CVM instance network access. You can perform the following actions:
    - Create and bind the default security group. You can preview the default security group rules.
    - Click **Add Security Group** to configure custom security group rules.
    For details, see [TKE Security Group Settings](https://intl.cloud.tencent.com/document/product/457/9084).
 - **Login Methods**: three login methods are available.
    - **SSH Key Pair**: A key pair is a pair of parameters generated by an algorithm. It is a more secure way to log in to a CVM instance than using regular passwords. For more details, refer to [SSH Keys](https://intl.cloud.tencent.com/document/product/213/6092).
    - **Random Password**: an automatically generated password will be sent to your [Message Center](https://console.cloud.tencent.com/message). 
    - **Custom Password**: Set a password as prompted.
2. Click **Next** to check and confirm the configuration information.
3. Click **Finish**.


<span id="RelatedOperations"></span>
## Relevant Operations
<span id="ServiceAuthorization"></span>
### Service authorization

1. When you log in to the [Tencent Cloud TKE console](https://console.cloud.tencent.com/tke2) for the first time, click **Clusters** in the left sidebar. The **Service authorization** page appears as shown in the following figure:

2. Click **Go to access management** to go to the **Role management** page.
3. Click **Grant authorization** and complete identity verification.
<span id="PVC"></span>
### Creating VPCs
1. Log in to the [VPC Console](https://console.cloud.tencent.com/vpc/vpc?rid=1). Select a region at the top of the VPC list and click **+New** to go to the **Create a VPC** page.

2. Enter the following information:
 - **VPC information**    
	- **Region**: region of the VPC.
	- **Name**: name of the VPC.
	- **IPv4 CIDR Block**: the VPC IPv4 CIDR block. You can use one of the following CIDR blocks. **If you have multiple VPCs and they need to communicate with one another, make sure their CIDR blocks do not overlap**.
		- `10.0.0.0` - `10.255.255.255` (mask range: 16 to 28)
		- `172.16.0.0` - `172.31.255.255` (mask range: 16 to 28)
		- `192.168.0.0` - `192.168.255.255` (mask range: 16 to 28)
 - **Original subnet information**
	- **Subnet name**: name of the subnet.
	- **IPv4 CIDR Block**: the subnet IPv4 CIDR block. **The cannot be modified after creation**. The subnet CIDR block must be the same as or a subset of the VPC CIDR block. For example, if the VPC CIDR block is `192.168.0.0/16`, the subnet CIDR block can be `192.168.0.0/16` or `192.168.0.0/17`.
	- **Availability Zone**: select a desired availability zone.
	- **Associated route table**: a subnet must be associated with a route table for traffic forwarding. The console provides a **Default** route table.
3. Click **OK** to create a VPC.
<span id="Subnet"></span>
### Creating subnets

1. Log in to the [VPC Console](https://console.cloud.tencent.com/vpc/vpc?rid=1) and click **Subnet** in the left sidebar.
2. In the **Subnet** page, click **+New** to go to the **Create a Subnet** page. Configure the Subnet Name, VPC IP Range, CIDR, Availability Zone, and associated route table.
3. (Optional) Click **+Add a line** to create multiple subnets.
4. Click **Create**.
<span id="NewSecurityGroup"></span>
### Creating security groups
You can create a security group and bind it to a cluster during the cluster creation process, or create a custom security group that better suits your needs. 
1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/index). Click **Security Group** in the left sidebar to go to the **Security Group** page.
2. Select a region at the top of the page and click **+New** to go to the **Create a security group** page. Configure the following:

 - **Template**: select a template that suits your needs, as shown below:
<table>
	<tr><th>Template</th><th>Description</th><th>Notes</th></tr>
	<tr><td>Open all ports</td><td>All ports are open to the public and private network. May present security issues.</td><td>-</td></tr>
	<tr><td>Open port 22, 80, 443, 3389 and the ICMP protocol</td><td>Port 22, 80, 443 and 3389, and the ICMP protocol are open. All ports are open to the private network.</td><td>Suitable for instances with web services.</td></tr>
	<tr><td>Custom</td><td>Creates a blank security group in which rules are added afterwards. For details on how to add rules, refer to <a href="https://intl.cloud.tencent.com/document/product/213/34272">Adding Security Group Rules</a>.</td><td>-</rd></tr>
</table>
 - **Name**: name of the security group.
 - **Project**: by default, **Default project** is selected. Select a project to facilitate management.
 - **Notes**: a short description of the security group.
 - **Display template rule**: click to reveal existing security group inbound and outbound rules.
3. Click **OK** to create the security group.
If you select **Custom** as the template for your security group, click **Add rules now** to [add security group rules](https://intl.cloud.tencent.com/document/product/213/34272).


### Creating SSH keys<span id="SSH"></span>

 1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/) and click [**SSH Key**](https://console.cloud.tencent.com/cvm/sshkey) in the left sidebar to go to the **SSH Key** page.
 2. Click **Create a key** to go to the **Create an SSH Key** page.
 3. Configure the following:

  - **Mode**: you can **Create a new key pair** or **Use an existing public key**.
        - If you select **Create a new key pair**, enter a name.
        - If you select **Use an existing public key**, enter the key name and the original public key information.
> The following is a sample public key:
>```
>ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCdv1zOdTqtt70iqgCBT6mYbwCP3ASSl6Qidr/LmBkMCbWvSB1PDcZhcVmnkM1Fcltz25UroRmusF6s45HOgU2qZtC4J1jPV1SG6ashUJgJw9TSmnHPvy76BcRFe4xwA75CVfozSqeJejLnHP1oF8Dj+cM7/DLmxbOpJO1kaIx2bVuqYrwQGah6L3nozKSTY9qZ6pBar8TJFmgp4YDaxso78oqBtt0Q82c9MWTMszt3VvfNscS2WY6PFF3OHOlwkUesfPez5OnUeeCFpD3T5UCfTY0yrjbcYqx4WHElZ92RtSNDTbonAxUPHVYi8r6tkVNznBJJ2E+6TphvGIR2wzPl skey-qswnaltn
>```
```

 4. Click **OK** to go to the *SSH Key Pair Created** page. Click **Download** to save a copy of the private key.
> Tencent Cloud does not save your private key. Download the private key within 10 minutes.


### Changing the default OS of a cluster
>
> Before changing the default OS of a cluster, read [Operating System Description](#OS) carefully to learn about the relevant risks.

1. Log in to the [Tencent Cloud TKE console](https://console.cloud.tencent.com/tke2) and click **Clusters** in the left sidebar.
2. On the **Cluster Management** page, select **More** -> **Query Cluster Credentials** for the target cluster to go to the basic information page of the cluster.
3. In **Node and Network Information**, click <img src="https://main.qcloudimg.com/raw/12834a28b9839ffe9a3723ca23ba19ce.png" style="margin:-3px 0px"> next to **Default OS**.

4. On the **Set Cluster OS** page, change the OS and click **Submit**.



```