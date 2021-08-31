 Virtual Private Clouds (VPCs) are the basis for using Tencent Cloud services. When you purchase an instance, such as a CVM, you need to choose the VPC to which the instance belongs. This document introduces the usage lifecycle of VPCs.

## Background

Based on different usage needs, the lifecycle of VPCs is shown in the figure below:
![](https://main.qcloudimg.com/raw/791bd82db5d80be627f45c98d1603b4f.png)

1. [Creating a VPC](#1): before creating a VPC, you need to carefully [plan your network](https://intl.cloud.tencent.com/document/product/215/31795). The CIDR blocks of VPCs and subnets cannot be modified after creation.
2. [Viewing a VPC](#2): you can view the basic information of a VPC, its CCN association, and the resources it contains.
3. (Optional) you can choose different operations based on actual use cases:
 - When the primary CIDR blocks are insufficient:
    - [Creating Auxiliary CIDR Blocks](#21): when the primary CIDR blocks are insufficient for allocation, you can create auxiliary CIDR blocks to meet your actual network demands.
    - [Deleting Auxiliary CIDR Blocks](#32): if auxiliary CIDR blocks are not needed, you can delete them.
 - If you need to use IPv6 addresses:
    -  [Assigning IPv6 CIDR Blocks](#31): if you need to use IPv6 addresses, you can create IPv6 CIDR blocks to meet your actual network demands.
    - [Releasing IPv6 CIDR Blocks](#22): if IPv6 CIDR blocks are not needed, you can release them. After release, the IPv6 addresses of all cloud resources in the VPC are released and cannot be recovered.
4. [Deleting a VPC](#3): after a VPC is deleted, the subnets and route tables in the VPC are also deleted.


<span id ="1"></span>

## Creating a VPC

A VPC must have at least one subnet, and Tencent Cloud service resources can only be added in a subnet.

1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. At the top of the “VPC” page, select a region, and click **+New**
3. In the “Create a VPC” dialog box, enter the VPC information and initial subnet information, and then click **OK**.

>? The CIDR blocks of the VPC and subnet cannot be modified after creation.

 - The VPC CIDR block can be any of the following IP ranges. For VPCs to communicate with each other over a private network, their CIDR blocks must not overlap.
  - `10.0.0.0` - `10.255.255.255` (mask range between 16 and 28)
  - `172.16.0.0` - `172.31.255.255` (mask range between 16 and 28)
  - `192.168.0.0` - `192.168.255.255` (mask range between 16 and 28)

 - The subnet CIDR block must be within or the same as the VPC CIDR block.
   For example, if the IP range of a VPC is `192.168.0.0/16`, then that of its subnets can be `192.168.0.0/16`, `192.168.0.0/17`, etc. 
   ![](https://main.qcloudimg.com/raw/a2aab5034960c9cfb517b053d4107c0f.png)

<span id ="2"></span>

## Viewing a VPC

1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Select the region of the VPC at the top of the “VPC” page.
3. In the VPC list, click the ID of the VPC that you want to view.
 On the details page, you can view the basic information of the VPC, its CCN association, and the resources it contains.
![](https://main.qcloudimg.com/raw/31fdffbfa34db31772b2bc87d280ac0c.png)

<span id ="21"></span>

## Creating Auxiliary CIDR Blocks

>?
>
>- Currently, the auxiliary CIDR block feature is in beta testing. If you want to use it, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=168&source=0&data_title=%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9CVPC&step=1) to apply.
>- The auxiliary CIDR block can overlap with the destination IP range of a custom route. However, you need to exercise caution with this, because the auxiliary CIDR block route is a local route and the priority of local routes is higher than that of custom subnet routes.
>- Classic network CVMs do not support interconnection with cloud resources in the auxiliary CIDR block.
>- Currently, only Cloud Connect Network (CCN) supports passing the auxiliary CIDR block. That is, CVMs in the auxiliary CIDR block cannot communicate with other VPCs or IDCs via peering connection or Direct Connect.

1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Select the region of the VPC at the top of the “VPC” page.
3. In the VPC list, click **Edit CIDR** in the **Operation** column on the right side of the target VPC.
4. In the “Edit CIDR” dialog box, click **Add** below IPv4 CIDR, enter the auxiliary CIDR block information, and then click **OK**.

<span id ="31"></span>

## Assigning IPv6 CIDR Blocks

>? Currently, EIPv6 is in beta testing. [Submit a beta application](https://intl.cloud.tencent.com/apply/p/c28sebss8v) if you want to use it.

1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Select the region of the VPC at the top of the “VPC” page.
3. In the VPC list, click **Edit CIDR** in the **Operation** column on the right side of the target VPC.
4. In the “Edit CIDR” dialog box, click **Obtain** on the right side of the IPv6 CIDR block and confirm the operation. Then, the system will assign one `/56` IPv6 CIDR block to the VPC.


<span id ="22"></span>

## Releasing IPv6 CIDR Blocks

>? Currently, EIPv6 is in beta testing. [Submit a beta application](https://intl.cloud.tencent.com/apply/p/c28sebss8v) if you want to use it.

1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Select the region of the VPC at the top of the “VPC” page.
3. In the VPC list, click **Edit CIDR** in the **Operation** column on the right side of the VPC for which an IPv6 CIDR block has been obtained.
4. In the “Edit CIDR” dialog box, click **Release** on the right side of the IPv6 CIDR block and confirm the operation. Then, the system will release the IPv6 CIDR block.  
    ![](https://main.qcloudimg.com/raw/f8eb3a5d86ac47a3046575d2330cfd58.png)

<span id ="32"></span>

## Deleting Auxiliary CIDR Blocks

>? Currently, the auxiliary CIDR block feature is in beta testing. If you want to use it, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=168&source=0&data_title=%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9CVPC&step=1) to apply.

1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Select the region of the VPC at the top of the “VPC” page.
3. In the VPC list, click **Edit CIDR** in the **Operation** column on the right side of the VPC for which you want to delete an auxiliary CIDR block.
4. In IPv4 CIDR block of the “Edit CIDR” dialog box, click **Delete** after the auxiliary CIDR block and confirm the operation.

<span id ="3"></span>

## Deleting a VPC

>? To delete a VPC there must be no occupation of the VPC’s IP addresses and no cloud resources in the VPC (such as CVMs, TencentDB instances, or gateways).

1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Select the region of the VPC at the top of the “VPC” page.
3. In the VPC list, click **Delete** in the **Operation** column on the right side of the VPC to be deleted.
