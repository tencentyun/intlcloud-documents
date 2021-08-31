## Overview
You can create a CVM instance on a purchased CDH instance through the console or an API.

## Prerequisites
To assign a CVM to a CDH instance, complete the following preparations as needed:
- To create a CVM instance whose network type is virtual private cloud (VPC), you need to [create a VPC](https://intl.cloud.tencent.com/document/product/215/31805) in the target region and [create a subnet](https://intl.cloud.tencent.com/document/product/215/31806) in the target availability zone under the VPC.
- If you do not use the default project, you need to [create a project](https://intl.cloud.tencent.com/document/product/378/34726).
- If you do not use the default security group, you need to [create a security group](https://intl.cloud.tencent.com/document/product/213/34271) in the target region and add a security group rule that meets your business requirements.
- To bind a SSH key pair when creating a Linux instance, you need to [create a SSH key](https://intl.cloud.tencent.com/document/product/213/16691) for the target project.
- To create a CVM instance with a custom image, you need to [create a custom image](https://intl.cloud.tencent.com/document/product/213/4942) or [import an image](https://intl.cloud.tencent.com/document/product/213/4945).

## Notes
The number of CVMs that can be created on a CDH instance depends on the CVM specifications and the available resources including CPU, memory, and local disk.
For example, a completely idle HS20 (56 cores and 224 GB memory) can be assigned with seven 8-core, 32 GB CVMs.

## Directions
### Creating a CVM via the console
#### Going to the CVM assignment page
1. Log in to the [Dedicated Hosts console](https://console.cloud.tencent.com/cvm/cdh).
2. On the **Dedicated Host** page, select a desired region. Under the region, select a CDH instance, and click **Assign CVM**, as shown below:
![Creating a CVM](https://main.qcloudimg.com/raw/84b0b73e84df7f5ad578ccffb2b45857.png)

#### Selecting CPU and memory configurations for CVMs
1. On the **1. Select the region and model** page, select the region, model, and other information.
![](https://main.qcloudimg.com/raw/46c568029c0ce3b9fc681d05f6994c4c.png)
Main parameters are described as follows:

 - **CPU**: you can customize the CVM CPU according to the remaining resources of the selected CDH or host resource pool.
 - **MEM**: you can customize the CVM memory according to the remaining resources of the selected CDH or host resource pool.
 >?The CVM configurations determine the number of CVMs that can be created.

2. Click **Next: Select an image**.

#### Selecting an image
1. On the **2. Select an image** page, select an image.
![](https://main.qcloudimg.com/raw/a4a3c3dd818d3867613865efdaa3d799.png)
Main parameters are described as follows:
 - **Image Provider**: Tencent Cloud provides three types of images, namely public images, custom images, and shared images. For more information, see [Image Types](https://intl.cloud.tencent.com/document/product/213/4941).
 - **Operating system**: select the operating system used in your environment.
 - **System version**: select the operating system version used in your environment.

2. Click **Next: Select storage and network**.

#### Selecting storage and network configurations
1. On the **Select storage and network** page, select the system disk and data disk, and configure network information.
![](https://main.qcloudimg.com/raw/0582941aeb03a8c5ce171e9c7b678f27.png)
Main parameters are described as follows:
 - **System disk**: this parameter is required. The system disk is used to install the operating system. Its default capacity is 50 GB. You can select a disk type and capacity as needed. The available disk types vary depending on the region selected.
 - **Data disk**: this parameter is optional. You can choose to add a data disk when or after creating an instance, and select the cloud disk type and capacity. You can also create an empty data disk or create a data disk using a data disk snapshot.
CVM supports local disks (HDD or SDD) and cloud disks (HDD, Premium Cloud Storage, and SSD) for storage. For more information about cloud disks, see [Cloud Disk Types](https://intl.cloud.tencent.com/document/product/362/31636).
 - **Network type**:
     - **Classic Network**: the classic network is unavailable for all accounts in regions that were activated after August 3, 2017 and some accounts that were registered after June 13, 2017.
     - **Virtual Private Cloud**: select a VPC and a subnet. If no existing VPC and subnet are available, select the default VPC and subnet. For more information about the classic network and VPC, see [Overview](https://intl.cloud.tencent.com/document/product/215/535).
   - **Public IP**: the network of CVMs on a CDH instance supports only bill-by-traffic. To assign a public IP to a CVM, select **Buy Now**. The public IP assigned in this way cannot be directly unbound from the instance. However, you can convert the public IP into an EIP and then unbind it from the instance.
   - **Public network bandwidth**: set this parameter based on your actual requirements.
   - **CVM Quantity**: set this parameter based on your actual requirements.
2. Click **Next: Set information**.

#### Setting information
1. On the **4. Set information** page, set the project, CVM name, and login method, and select a security group.
![](https://main.qcloudimg.com/raw/bb8115f15f0279e6a39a8bd526307a31.png)
Main parameters are described as follows:
 - **CVM Name**:
    - If you select **Name after creation**, the name of the CVM after creation will be **Unnamed**, which is displayed only on the console and is not the host name of the CVM.
    - If you select **Name It Now**, enter a meaningful name within 60 characters.
 - **Login Methods**:
     - For CVMs with Linux images, the options include **Set Password**, **SSH Key Pair**, and **Automatic password generation**.
     - For CVMs with Windows images, the options include **Set Password** and **Automatic password generation**.
 - **Security Groups**:
     - If no security group is available, click **Create a security group**.
     - If there are available security groups, select an existing one. You can also preview the security group rules. For more information about security group rules, see [Security Group](https://intl.cloud.tencent.com/document/product/213/12452).
 - **Security Service**: by default, DDoS Protection, Web Application Firewall (WAF), and Cloud Workload Protection are activated for free. For more information, see [Product Introduction](https://intl.cloud.tencent.com/document/product/296/2221).
 - **Cloud Monitoring**: by default, cloud monitoring is enabled for free. You can install Cloud Monitor to obtain CVM monitoring metrics and display them in visual charts. You can also specify custom alarm thresholds. For more information, see [Product Overview](https://intl.cloud.tencent.com/document/product/248/32799).
2. Click **Buy Now**.
>?After the CVM is created, go to the Message Center and receive information such as instance name, public IP, private IP, login name, and initial login password (if you choose the login method **Automatic password generation**). You can use these information to log in to and manage instances.
>


### Creating a CVM via an API
Use the [`RunInstances`](https://intl.cloud.tencent.com/document/product/213/33237) API to create CVM instances on a specified CDH instance.


