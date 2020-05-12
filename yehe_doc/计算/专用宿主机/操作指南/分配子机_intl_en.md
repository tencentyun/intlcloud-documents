## Scenario
You can create a CVM instance on a purchased CDH instance through the console or API.

## Prerequisites
Before assigning a dedicated CVM on a CDH instance, complete the following steps:
- To create a CVM instance whose network type is virtual private cloud (VPC), you need to [create a VPC](https://intl.cloud.tencent.com/document/product/215/31805) in the target region, and [create a subnet](https://intl.cloud.tencent.com/document/product/215/31806) in the target availability zone (AZ) under the VPC.
- If you do not use the default project created automatically by the system, you need to [create a project](https://intl.cloud.tencent.com/document/product/378/34726).
- If you do not use the default security group, you need to [create a security group](https://intl.cloud.tencent.com/document/product/213/34271) in the target region and add a security group rule that satisfies your business requirements.
- To bind an SSH key pair when creating a Linux instance, you need to [create SSH keys](https://intl.cloud.tencent.com/document/product/213/16691) for the target project.
- To create a dedicated CVM with a custom image, you need to [create custom images](https://intl.cloud.tencent.com/document/product/213/4942) or [import an image](https://intl.cloud.tencent.com/document/product/213/4945).

## Note
The number of dedicated CVMs that can be created on a CDH instance depends on the dedicated CVM specifications and the remaining amount of available CPU, memory, local disk resources.
For example, a completely idle HS20 (56 cores and 224 GB memory) can be assigned with seven 8-core, 32 GB dedicated CVMs.

## Directions
### Creating a dedicated CVM through the console
#### Going to the dedicated CVM assignment page
1. Log in to the [Dedicated Hosts Console](https://console.cloud.tencent.com/cvm/cdh).
2. On the **Dedicated Host** page, select a desired region. Under the region, select a CDH instance, and click **Assign CVM**.
![Assigning a CVM](https://main.qcloudimg.com/raw/9113542c2cab5258892c73c4be64a701.png)

#### Selecting dedicated CVM configurations (such as CPU and memory)
1. On the **1. Select region and model** page, select the region, model, and other information.
![](https://main.qcloudimg.com/raw/a610583b4cb8c130a117e7825a4f4c40.png)
The main parameters are described as follows:
 - **CPU**: customize the dedicated CVM CPU according to the remaining resources of the selected host or host resource pool.
 - **MEM**: customize the dedicated CVM memory according to the remaining resources of the selected host or host resource pool.
 >The dedicated CVM configurations determine the number of dedicated CVMs that can be created.

2. Click **Next: Select an image**.

#### Selecting an image
1. On the **2. Select an Image** page, select an image.
![](https://main.qcloudimg.com/raw/5a7d3ebc85da72280cd769c9046e1581.jpg)
The main parameters are described as follows:
 - **Image Provider**: based on the sources, images provided by Tencent Cloud are divided into public images, custom images, and shared images. For more information, see [Image Types Overview](https://intl.cloud.tencent.com/document/product/213/4941).
 - **Operating system**: select the operating system used in your environment.
 - **System version**: select the operating system version used in your environment.
 
2. Click **Next: Select storage and network**.

#### Selecting storage and network configurations
1. On the **Select storage and network** page, select the system disk and data disk, and configure network information.
![](https://main.qcloudimg.com/raw/d6624835fc0aed2a315ddee0641013b2.png)
![](https://main.qcloudimg.com/raw/044ed130ea9bbff02664ef0b3b0e0b53.png)
The main parameters are described as follows:
 - **System disk**: this parameter is required. The system disk is used for installing the operating system and is 50 GB by default. You can select a disk type and capacity as needed. The disk types available vary depending on the region selected.
 - **Data disk**: this parameter is optional. You can choose to add a data disk after creating an instance; you can add a data disk at the time of purchase, and select the cloud disk type and capacity of the data disk; you can also create an empty data disk or create a data disk using a data disk snapshot.
Storage types supported by dedicated CVMs include local disks (HDDs or SSDs) and cloud disks (SSD Cloud Storage, Premium Cloud Storage, and HDD Cloud Storage). For more information about cloud disks, see [Cloud disk types](https://intl.cloud.tencent.com/document/product/362/31636).
 - **Network type**
     - **Basic Network**: the basic network is unavailable for all accounts in regions that were activated after August 3, 2017 and some accounts that were registered after June 13, 2017.
     - **Virtual Private Cloud**: select a VPC and a subnet. If no existing VPC and subnet are available, select the default VPC and subnet. For more information about the basic network and VPC, see [Overview](https://intl.cloud.tencent.com/document/product/215/535).
   - **Public IP**: the network of dedicated CVMs on a CDH instance supports only bill-by-traffic. To assign a public IP to a dedicated CVM, select **Buy Now**. The public IP assigned in this way cannot be directly unbound from the instance. However, you can convert the public IP into an EIP and then unbind it from the instance.
   - **Public network bandwidth**: set this parameter according to the specific requirements of your scenario.
   - **Number of Servers**: set this parameter according to the specific requirements of your scenario.
2. Click **Next: Set information**.

#### Setting information
1. On the **4. Set information** page, set the project, host name, and login method, and select a security group.
![](https://main.qcloudimg.com/raw/20ba29ea87e44cd2d0d7cdde37737c69.png)
The main parameters are described as follows:
 - **Host Name**:
    - If you select **Name after creation**, the name of the CVM after creation is **Unnamed**, which is displayed only on the console and is not the host name of the CVM.
    - If you select **Name It Now**, enter a semantic name with no more than 60 characters.
 - **Login Methods**:
     - For CVMs with Linux images, you can choose **Custom Password**, **SSH Key Pair**, or **Random Password** as the login method.
     - For CVMs with Windows images, you can choose **Custom Password** or **Random Password** as the login method.
 - **Security Groups**:
     - If no security group is available, select **Create a security group**.
     - If there are available security groups, select **Existing security groups**. You can also preview the security group rules. For more information about security group rules, see [Security Groups](https://intl.cloud.tencent.com/document/product/213/12452).
 - **Security Reinforcement**: by default, anti-DDoS protection, Web Application Firewall, and Cloud Workload Protection are enabled for free. For more information, see [Product Introduction](https://intl.cloud.tencent.com/document/product/296/2221).
 - **Cloud Monitoring**: by default, cloud monitoring is enabled for free. You can install Cloud Monitor to obtain CVM monitoring metrics and display them in visual charts. You can also customize alarm thresholds. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/248/32799).
2. Click **Buy Now**.
>After the CVM is created, you will receive an internal message containing information such as instance name, public IP, private IP, login name, and initial login password (if you choose the login method **Random Password**). You can use the information to log in to and manage instances.
>


### Creating a dedicated CVM through an API
You can use the RunInstances API to create a dedicated CVM for a CDH instance. For more information, see [RunInstances](https://intl.cloud.tencent.com/document/product/213/33237).
