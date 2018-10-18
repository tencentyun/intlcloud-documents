You can create CVM instances on the purchased CDH in the console or through the API.

## Prerequisites
Before assigning a dedicated CVM instance on the host, you need to complete the following tasks according to the actual situation:
- To create a VPC-type CVM instance, you need to [create a VPC](https://cloud.tencent.com/document/product/215/8113) in the target region and [create a subnet](https://cloud.tencent.com/document/product/215/8114) in the target availability zone on the VPC.
- If you don't want to use the default project created automatically by the system, you need to [create a project](https://cloud.tencent.com/document/product/378/8192).
- If you don't want to use the default security group created automatically by the system, you need to [create a security group](https://cloud.tencent.com/document/product/213/12450) in the target region and add security group rules that meet your business needs.
- When creating a Linux-based instance, you need to bind an SSH key pair by [creating an SSH key](https://cloud.tencent.com/document/product/213/516) for the target project.
- When creating a dedicated CVM instance with custom image, you need to [create a custom image](https://cloud.tencent.com/document/product/213/4942) or [import an image](https://cloud.tencent.com/document/product/213/4945).

## Creating a Dedicated CVM Instance in Console

1. Enter the instance assigning page.
1). Log in to the [CDH Console](https://console.cloud.tencent.com/cvm/cdh).
2). Select a region, check the CDH and click **Assign CVM**.
![CVM creation entry](https://main.qcloudimg.com/raw/449fd0352f70f7b530ff0e3c5b8b667c.png)

2. Select the instance CPU and memory configuration.
You can customize the CPU and memory configuration of the instance subject to the remaining available resources of the host/host resource pool you select. The instance resource configuration you specify will affect the number of instances that can be created.
![Setting CPU and memory](https://main.qcloudimg.com/raw/19246bbf58a97cdc1d8f9dc025068983.png)

3. Select an image.
According to different sources, Tencent Cloud provides the following image types: public image, custom image and shared image. For more information on image types, see [Introduction to Image Types](https://cloud.tencent.com/document/product/213/4941).
![Selecting an image](https://main.qcloudimg.com/raw/687824b62a6647f17e9efce72bea0b4e.png)

4. Select system disk and data disk.
The storage types supported by the instance include: local HDD/local SSD, HDD cloud disk, premium cloud disk and SSD cloud disk.
For more information on cloud disks, see [Cloud Disk Types](https://cloud.tencent.com/document/product/362/2353).
 - System disk: Required, for installing the operating system. You can select the type and capacity of the cloud disk used as the system disk. Available cloud disk types vary by the region selected. The default capacity of the system disk is 50 GB.
 - Data disk: Optional. You can add a data disk after creating the instance or add a data disk at the time of purchase and then select the type and capacity. You can create an empty data disk or create a data disk using a data disk snapshot.
![Selecting disk type](https://main.qcloudimg.com/raw/d6624835fc0aed2a315ddee0641013b2.png)

5. Set network information.
The instance subnet on the CDH only supports billing by traffic. If you want to assign a public IP address to the instance, you need to select **Purchase Now**. The IP address assigned in this way cannot be directly unbound from the instance; instead, it can be converted into an elastic public IP first and then unbound.
 - Basic network: Starting from August 3, 2017, newly launched regions no longer support basic network for all users. Some accounts registered after June 13, 2017 don't support basic network either.
 - VPC: VPC and subnet must be selected. If there are no VPC or subnet created in advance, the default VPC and subnet can be selected. For more information on basic network and VPC, see [VPC Overview](https://cloud.tencent.com/document/product/215/535).
![Setting up network](https://main.qcloudimg.com/raw/044ed130ea9bbff02664ef0b3b0e0b53.png)

6. Determine the number of instances.

7. Set the project, host name, login method and security group.
 - Host name:
     - You can select **Name It Now** at the time of purchase and enter a meaningful name of up to 60 characters.
     - You can also select **Name after creation**, and the name of the created CVM instance is "unnamed". This name is only displayed in the console and not the hostname of the instance.
 - Login method:
     - For CVM instances with Linux-type image, available login methods include **Set Password**, **SSH Key Pair** and **Random Password**.
     - For CVM instances with Windows-type image, available login methods include *Set Password** and **Random Password**.
 - Security group:
     - If you have not created a security group, select **Create a security group**;
     - If you already have a security group, select **Select a security group**.
Meanwhile, you can preview the security group rules. For more information, see [Security Group](https://cloud.tencent.com/document/product/213/5221).
![Host information](https://main.qcloudimg.com/raw/20ba29ea87e44cd2d0d7cdde37737c69.png)

8. Select security reinforcement and Cloud Monitor components.
 - Security reinforcement: DDoS protection, WAF and Host Security are activated free of charge. For more information, see [Host Security](https://cloud.tencent.com/document/product/296/2221).
 - Cloud Monitor: Cloud product monitoring is activated free of charge. Components are installed to obtain host monitoring metrics displayed as monitoring icons. Plus, custom alarm thresholds can be configured. For more information, see [Cloud Monitor Overview](https://cloud.tencent.com/document/product/248/13466).

> After the CVM instance is created, you will receive a message including the instance name, public IP address, private IP address, login name and the initial password (if Random Password is selected) which can be used to log in and manage the instance.

## Creating a Dedicated CVM Instance Through API
You can use the RunInstances API to create a dedicated CVM instance on a CDH. For instructions, see [API for Creating Instance](https://cloud.tencent.com/document/api/213/15730).
