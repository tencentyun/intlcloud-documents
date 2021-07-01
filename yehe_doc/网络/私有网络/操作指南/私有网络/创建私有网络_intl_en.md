Virtual Private Clouds (VPCs) are the basis for using Tencent Cloud services. When purchasing an instance such as CVM, CLB or TencentDB in a region that does not have existing VPCs, a default VPC and subnet will be automatically created. 
![](https://main.qcloudimg.com/raw/b2347dc036ba8f1ac6f5863c10dd1ad3.png)
The default VPC and subnet is created together with your instance, and do not count against your quota in the region. They work the same as the manually-created ones. There can only be one default VPC and subnet in each region. You can delete the default VPC and subnet if you no longer need them.
![](https://main.qcloudimg.com/raw/1b87531272cf8155fe0bbea6a1a74156.png)
![](https://main.qcloudimg.com/raw/a6910004b96d0bc0eaeec54ef52eb751.png)
You can refer to this document to create a VPC instance on the console if the default or existing ones are not suitable.

## Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Select a region at the top of the **VPC** page, and click **+New**.
3. Enter the VPC information and subnet information in the **Create VPC** pop-up dialog.
>?The CIDR blocks of the VPC and subnet cannot be modified after creation.
>
 - The VPC CIDR block can be any of the following IP ranges. For VPCs to communicate with each other over a private network, their CIDR blocks should not overlap.
    - `10.0.0.0` - `10.255.255.255` (mask range between 16 and 28)
    - `172.16.0.0` - `172.31.255.255` (mask range between 16 and 28)
    - `192.168.0.0` - `192.168.255.255` (mask range between 16 and 28)
 - The subnet CIDR block must fall within or be the same as the VPC CIDR block.
   For example, if the VPC IP range is `10.0.0.0/16`, then its subnet IP range can be `10.0.0.0/16`, `10.0.0.0/24`, etc.
 - Availability zone: a subnet is specific to availability zone. Select an availability zone in which the subnet resides. A VPC allows subnets in different availability zones, and these subnets can communicate with each other via a private network by default.
 - Associated route table: the subnet must be associated with a route table for traffic forwarding. A default route table will be associated to ensure private network interconnection in the VPC.
 - Advanced options: you can add tags to better manage resource permissions of sub-users and collaborators.
 <img src="https://main.qcloudimg.com/raw/c6a539df40bf88aa6fffda556fc639ba.png" width=50%></img>
4. After completing the configurations, click **OK**. A successfully created VPC will be displayed in the list, as shown below. A new VPC has a subnet and a default route table.
![](https://main.qcloudimg.com/raw/e6197fba795a2a750e12e8f392afba7c.png)

## Subsequent Operation
After the VPC and subnet have been created, you can deploy resources including CVM and CLB within the VPC.
Click the icon as shown below to directly purchase a CVM on the CVM purchase page. For more information, see [Building Up an IPv4 VPC](https://intl.cloud.tencent.com/document/product/215/31891).
![](https://main.qcloudimg.com/raw/a55d21c5b5be82f375370a7eaf3529ec.png)
