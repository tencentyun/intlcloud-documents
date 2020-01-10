## Cross-AZ Access in a VPC

If you need to have a CFS instance shared by multiple CVM instances in different AZs in the same region, you can configure the CVM and CFS instances into the same VPC to achieve cross-AZ access to resources.

For example, assume that there is a CVM instance in Guangzhou Zone 1 that needs to use CFS, but file systems cannot be directly created in Guangzhou Zone 1 as the resources are sold out there.
If the CVM instance is in the "Guangzhou Zone 1" subnet of a VPC, you can log in to the [VPC Console](https://console.cloud.tencent.com/vpc) to create a subnet whose AZ is "Guangzhou Zone 2" for the VPC.
![](https://main.qcloudimg.com/raw/d25fc9283b76f114a772bebb1b703548.png)
![](https://main.qcloudimg.com/raw/74ffa38cc8774e6534617aed6f4476df.png)
![](https://main.qcloudimg.com/raw/344f0c3bfce47031137fa66351bbb11c.png)

After the subnet is successfully created, go back to the CFS Console and select this VPC and the subnet you just created to create resources in Guangzhou Zone 2. The CFS file system can be directly mounted to the CVM instance in the subnet of Guangzhou Zone 1 in this VPC. For more information, please see [Using CFS File Systems on Linux Clients](https://intl.cloud.tencent.com/document/product/582/11523).


## Cross-VPC and Cross-region Access
CFS supports the following scenarios for resource access.

- You need to have the CFS instance shared by multiple CVM instances distributed in different VPCs; 
- Your CVM and CFS instances are in different VPCs;
- Your CVM and CFS instances are in different regions (for better access performance, it is recommended that the CVM instances and CFS be in the same region);

You can achieve resource access across the CVM instances distributed in VPC-A/VPC-B and CFS instance distributed in VPC-C by configuring a "peering connection". For more information, please see [Peering Connection](https://intl.cloud.tencent.com/document/product/215/5000).


## Cross-network Access
If you need to have a CFS instance shared by multiple CVM instances distributed in the basic network and a VPC, you can create a CFS file system in the VPC.
- From CVM instances in the basic network to CFS in a VPC: mutual access to resources between a CVM instance in the basic network and resources in a VPC can be achieved by configuring a "Classiclink". For more information, please see [Classiclink Settings](https://cloud.tencent.com/document/product/215/20083).
- From CVM instances in VPC-A to CFS in VPC-B: please refer to the setting method above.

>
>- Currently, CFS instances in the basic network cannot be connected to CVM instances in VPCs.
>- The client and CFS instance are in the basic network and a VPC, respectively, but they cannot be connected if they are in different regions.
