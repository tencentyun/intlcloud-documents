VPCs provide a basis for using Tencent Cloud services. This document describes how to create a VPC in the VPC console.

## Operation Guide
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Select the region of the VPC at the top of the **VPC** page and click **Create**.
3. In the **Create VPC** pop-up window, enter the VPC information and initial subnet information.
>?The CIDR blocks of the VPC and subnet cannot be modified after creation.
>
 - The VPC CIDR block can be any of the following IP ranges. For VPCs to communicate with each other over a private network, their CIDR blocks should not overlap.
    - `10.0.0.0` - `10.255.255.255` (the mask range must be 12–28)
    - `172.16.0.0` - `172.31.255.255` (the mask range must be 12–28)
    - `192.168.0.0` - `192.168.255.255` (the mask range must be 16–28)
 - The subnet CIDR block must fall within or be the same as the VPC CIDR block.
   For example, if the VPC IP range is `10.0.0.0/16`, then its subnet IP range can be `10.0.0.0/16`, `10.0.0.0/24`, etc.
 - AZ: A subnet is specific to an AZ. Select an AZ where the initial subnet resides. A VPC allows for subnets in different AZs. By default, these subnets can communicate with each other over the private network.
 - **Associated route table**: The subnet must be associated with a route table for traffic forwarding. The initial subnet is associated with a default route table that is delivered by the system by default to indicate interconnection in the VPC.
 - **Advanced options**: You can add tags as needed to better manage the resource permissions of sub-users and collaborators.
 <img src="" width=50%></img>
4. After completing the configuration, click **OK**. The successfully created VPC is displayed in the list, which has an initial subnet and a default route table as shown below.
![](https://main.qcloudimg.com/raw/269317b3b2b8220fde33fd01e77be65e.png)

## Subsequent Operations
After creating the VPC and initial subnet, you can deploy resources such as CVM and CLB instances within the VPC.
Click the icon as shown below to directly purchase a CVM instance on the CVM purchase page. For more information, see [Building Up an IPv4 VPC](https://intl.cloud.tencent.com/document/product/215/31891).
![](https://main.qcloudimg.com/raw/8374f8704f9ac1731ba84eb9d3570254.png)


## Related Content
There is a default VPC; that is:
When no VPCs are created in a region, you can select the default VPC and subnet created by Tencent Cloud when creating a CVM, CLB, or TencentDB instance in the region as shown below.
![](https://main.qcloudimg.com/raw/98878feb887075f6535eca50a76d3d0c.png)
The default VPC and subnet are created together with your instance and do not count towards your quota in the region. They work the same as the manually created ones. There can be only one default VPC in a region and only one default subnet in an AZ. The default VPC and subnet can be deleted if no longer needed.
![](https://main.qcloudimg.com/raw/a67ac7a3ac09b41905e11925f11bfa51.png)
![](https://main.qcloudimg.com/raw/907d836a6fe2e41ec2dc6a9b2796ad3a.png)

