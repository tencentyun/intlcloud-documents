Virtual Private Clouds (VPCs) are the basis for using Tencent Cloud services. When purchasing an instance such as CVM, CLB or TencentDB in a region that does not have existing VPCs, a default VPC and subnet will be automatically created. 
![](https://main.qcloudimg.com/raw/98878feb887075f6535eca50a76d3d0c.png)
The default VPC and subnet are created together with your instance, and do not count against your quota in the region. They work the same as the manually-created ones. There can only be one default VPC and subnet in each region. You can delete the default VPC and subnet if you no longer need them.
![](https://main.qcloudimg.com/raw/a67ac7a3ac09b41905e11925f11bfa51.png)
![](https://main.qcloudimg.com/raw/907d836a6fe2e41ec2dc6a9b2796ad3a.png)
You can refer to this document to create a VPC instance on the console if the default or existing ones are not suitable.

## Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Select a region at the top of the **VPC** page, and click **+New**.
3. Enter the VPC information and subnet information in the **Create VPC** pop-up.
>?The CIDR blocks of the VPC and subnet cannot be modified after creation.
>
 - The VPC CIDR block can be any of the following IP ranges. For VPCs to communicate with each other over a private network, their CIDR blocks should not overlap.
    - `10.0.0.0` - `10.255.255.255` (mask range between 16 and 28)
    - `172.16.0.0` - `172.31.255.255` (mask range between 16 and 28)
    - `192.168.0.0` - `192.168.255.255` (mask range between 16 and 28)
 - The subnet CIDR block must fall within or be the same as the VPC CIDR block.
   For example, if the VPC IP range is `10.0.0.0/16`, then its subnet IP range can be `10.0.0.0/16`, `10.0.0.0/24`, etc.
 - Availability zone: a subnet is specific to availability zone. Select an availability zone in which the subnet resides. A VPC allows for subnets in different availability zones and by default these subnets can communicate with each other via a private network.
 - Associated route table: the subnet must be associated with a route table for traffic forwarding. A default route table will be associated to ensure private network interconnection in the VPC.
 - Advanced options: you can add tags to better manage resource permissions of sub-users and collaborators.
4. After completing the configurations, click **OK**. A successfully created VPC will be displayed in the list, as shown below. A new VPC has a subnet and a default route table.
![](https://main.qcloudimg.com/raw/269317b3b2b8220fde33fd01e77be65e.png)

## Subsequent Operation
After the VPC and subnet have been created, you can deploy resources including CVM and CLB within the VPC.
Click the icon as shown below to directly purchase a CVM on the CVM purchase page. For more information, see [Building Up an IPv4 VPC](https://intl.cloud.tencent.com/document/product/215/31891).
![](https://main.qcloudimg.com/raw/8374f8704f9ac1731ba84eb9d3570254.png)
