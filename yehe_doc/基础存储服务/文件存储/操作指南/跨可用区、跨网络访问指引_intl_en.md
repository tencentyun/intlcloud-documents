## Cross-AZ Access in a VPC

If you need to have a CFS instance shared by multiple CVM instances in different AZs in the same region, you can configure the CVM and CFS instances into the same VPC to achieve cross-AZ access to resources.

For example, assume that there is a CVM instance in Guangzhou Zone 1 that needs to use CFS, but file systems cannot be directly created in Guangzhou Zone 1 as the resources are sold out there.
If the CVM instance is in the "Guangzhou Zone 1" subnet of a VPC, you can log in to the [VPC Console](https://console.cloud.tencent.com/vpc) to create a subnet whose AZ is "Guangzhou Zone 2" for the VPC.
![](https://main.qcloudimg.com/raw/98f9e310bbf48820bb8781ed01c89fcd.png)
![](https://main.qcloudimg.com/raw/ef4d81e3d728c3bef173aaf2c1f59551.png)
![](https://main.qcloudimg.com/raw/28b51682e19077de58c6c0e9a86e1d11.png)

After the subnet is successfully created, go back to the CFS Console and select this VPC and the subnet you just created to create resources in Guangzhou Zone 2. The CFS file system can be directly mounted to the CVM instance in the subnet of Guangzhou Zone 1 in this VPC. For more information, please see [Using CFS File Systems on Linux Clients](https://intl.cloud.tencent.com/document/product/582/11523).


## Cross-VPC and Cross-Region Access
CFS supports the following scenarios for resource access.

- You need to have the CFS instance shared by multiple CVM instances distributed in different VPCs; 
- Your CVM and CFS instances are in different VPCs;
- Your CVM and CFS instances are in different regions (for better access performance, it is recommended that the CVM instances and CFS be in the same region).

You can achieve resource access across the CVM instances distributed in VPC-A/VPC-B and CFS instance distributed in VPC-C by configuring a "peering connection". For more information, please see [Configuring the Route to Peering Connection](https://intl.cloud.tencent.com/document/product/553/19696).


## Cross-Network Access
If you need to have a CFS instance shared by multiple CVM instances distributed in the basic network and a VPC, you can create a CFS file system in the VPC.
- From CVM instances in the basic network to CFS in a VPC: mutual access to resources between a CVM instance in the basic network and resources in a VPC can be achieved by configuring a "Classiclink". For more information, please see [Enabling Cross-region Connectivity for Basic Networks](https://intl.cloud.tencent.com/document/product/553/18850).
- From CVM instances in VPC-A to CFS in VPC-B: please refer to the setting method above.

>!
>- Currently, CFS instances in the basic network cannot be connected to CVM instances in VPCs.
>- The client and CFS instance are in the basic network and a VPC, respectively, but they cannot be connected if they are in different regions.
