This document introduces the custom configuration of a Linux CVM.
Different from quick configuration, custom configuration provides full options, and you can choose the appropriate configuration based on your needs.

<div id="page1"></div>

## Prerequisites
 1. Before starting the custom configuration, you need to complete Step 1 in [**Getting Started with Linux CVM**](https://intl.cloud.tencent.com/document/product/213/2936).
 2. Go to the Tencent Cloud official website, select **Products** -> **Cloud Compute & Network** -> **Cloud Virtual Machine**, and click **Buy Now** to enter the [CVM purchase page](https://buy.cloud.tencent.com/buy/cvm).
 3. Click **Custom Configuration** to go to the custom configuration page.

<div id="page2"></div>

## Selecting Region and Model
![image-20181010153405408](https://main.qcloudimg.com/raw/a71d4168ae6bd2b762badd4689c0aba7.png)
 1. Select the Postpaid billing method (users who cannot purchase postpaid CVMs need to complete [Identity Verification](https://console.cloud.tencent.com/developer/infomation) first).

 2. Select a region and an availability zone. When you need more than one CVM, it is recommended that you choose different availability zones to implement disaster recovery.

 3. Select a model and configuration.
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Based on different underlying hardware, Tencent Cloud offers two series of instances: **Series 1** and **Series 2** (also referred to as **last-generation instance** and **current-generation instance**). They respectively provide the following instance types:

- Last-generation instance types: Standard S1, High IO I1, and MEM Optimized M1
- Current-generation instance types: [Standard S2](https://intl.cloud.tencent.com/document/product/213/11518#S2), [High IO I2](https://intl.cloud.tencent.com/document/product/213/11518#I2), [MEM Optimized M2](https://intl.cloud.tencent.com/document/product/213/11518#M2), [Computing C2](https://intl.cloud.tencent.com/document/product/213/11518#C2), [GPU-based GN2](https://intl.cloud.tencent.com/document/product/213/11518#GN2), and [FPGA-based FX2](https://intl.cloud.tencent.com/document/product/213/11518#FX2) 
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;It is recommended that you create an instance using a current-generation instance type to achieve optimal performance. For more information, see [Instance Types](https://intl.cloud.tencent.com/document/product/213/11518).

>Note:
>Series and models vary with different areas and availability zones.

Click **Next Step: Select Image** to enter the image selection page.

<div id="page3"></div>

## Selecting an Image
![image-20181009174332701](https://main.qcloudimg.com/raw/672968dca61a9a48cd935c0f3d7f00cf.png)
 1. Select an image provider.
Tencent Cloud supports public images, custom images, shared images, and service marketplace images. Select one by referring to [Image Types](https://cloud.tencent.com/document/product/213/4941).
We recommend that users who have just started using Tencent Cloud select public images.

 2. Select an operating system.
Tencent Cloud provides various operating systems such as CentOS, CoreOS, Debian, FreeBSD, OpenSUSE, SUSE, and Ubuntu. You need to build a subsequent operating environment on your own.

 3. Select a system version. 

Click **Next Step: Select Storage and Network** to enter the storage and network selection page.

<div id="page4"></div>

## Selecting Storage and Network
![](https://main.qcloudimg.com/raw/5cfedc485adae3943823ed7920f26aad.png)
 1. Select the type of disk and the size of data disk.
Tencent Cloud provides cloud disk, local disk and SSD cloud disk (The system disk size is optional, which defaults to 50 GB).
  - Cloud disk: Deliver high data reliability with the distributed three-copy mechanism.
  - SSD cloud disk: Built upon the full NVMe SSD storage media and Tencent Cloud's CBS 3-copy distributed storage technology, an SSD cloud disk provides I/O capabilities featured by low latency, high random IOPS and high throughput, and high-performance storage with 99.9999999% data security. It is applicable to scenarios which require high IO performance.
  - Local disk: A storage located on the physical machine where the CVM resides, which allows low latency but may cause single point of failure risk. For the comparison, see [Product Category](https://intl.cloud.tencent.com/document/product/213/4952).

 2. Select a network type.
Tencent Cloud provides two network types: basic network and VPC.
- Basic network: Suitable for new users. CVMs of the same user are interconnected via a private network.
- VPC: Suitable for advanced users. Different VPCs are logically isolated from each other.
	>**Note:**
	> Public network gateway is an interface between a VPC and a public network, which can forward requests from CVMs without public IP in different subnets of the VPC. For more information, see [Public Gateway](http://cloud.tencent.com/doc/product/215/%E7%BD%91%E5%85%B3#1.-公网网关).

 3. Select public network bandwidth.
Tencent Cloud provides two options: Bill-by-bandwidth or Bill-by-traffic.
- Bill-by-bandwidth: Select a fixed bandwidth. Packet loss occurs if this bandwidth is exceeded. This is suitable for scenarios with minor network fluctuation.
- Bill-by-traffic: The service is charged based on the actual traffic usage. You can set a limit for peak bandwidth to avoid extra fees caused by unplanned traffic. Packet loss occurs when the instantaneous bandwidth exceeds this limit. This is suitable for scenarios with large network fluctuations.

  4. Select quantity.


Click **Next Step: Set Information** to enter the information setting page.

<div id="page5"></div>

## Setting Information
![image-20181009174512418](https://main.qcloudimg.com/raw/a52108b18b1ab2313a8b92661e3e4782.png)
 1. Set a CVM name: You can choose **Name It after Creation** or **Name It Now**.

 2. Set login information:
- Set a password: Enter a CVM password.
- Associate a key now: Associate an SSH key. If you do not have a key or have an invalid key, click **Create Now** to create one. For more information, see [Creating Key](https://intl.cloud.tencent.com/document/product/213/16691#creating-an-ssh-key). For more information on the SSK key, see [SSH Key](<https://intl.cloud.tencent.com/document/product/213/16691>).
- A system-generated password is sent to you via internal message.

 3. Select a security group (**Make sure that the login port 22 is enabled**. For more information, see [Security Group](https://intl.cloud.tencent.com/document/product/213/15377)).

Click the **Enable** button to log in to the [Console](https://console.cloud.tencent.com/cvm) to check your CVM.

After the CVM is created, you will receive an internal message containing the instance name, public IP, private IP, login name, initial login password, and other information. You can use these information to log in to and manage your instance. To ensure the security of your CVM, change your Linux login password as soon as possible.

Click [here](https://cloud.tencent.com/document/product/213/2936#.E6.AD.A5.E9.AA.A4.E4.B8.89.EF.BC.9A.E7.99.BB.E5.BD.95-linux-.E4.BA.91.E6.9C.8D.E5.8A.A1.E5.99.A8) to complete subsequent configurations, including logging in to the Linux CVM, formatting and partitioning the data disk.

