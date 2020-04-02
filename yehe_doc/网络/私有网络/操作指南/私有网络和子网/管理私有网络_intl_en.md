When no VPC is available, the system will create a default VPC for you in the corresponding region after you purchase an instance (for example, a CVM). The default VPC can help you deploy business efficiently.

The default VPC has the same features as a custom VPC that you create. In addition, the default VPC does not consume your regional quota. When you no longer need the default VPC, you can delete it by yourself.

## Creating a VPC
A VPC contains at least one subnet. Cloud service resources can only be added to subnets.
1. Log in to [VPC Console](https://console.cloud.tencent.com/vpc).
2. Select the region of the VPC at the top of the list and click **+Create**.
3. Enter the VPC information and the initial subnet information, and click **Create**. The CIDR blocks of VPC instances and subnets cannot be modified once created.
 - The CIDR of a VPC can use any of the following IP ranges. To communicate between different VPC instances, ensure that the CIDR settings of both ends do not overlap with each other.
    - `10.0.0.0` - `10.255.255.255` (The mask must range from 16 to 28.)
    - `172.16.0.0` - `172.31.255.255` (The mask must range from 16 to 28.)
    - `192.168.0.0` - `192.168.255.255` (The mask must range from 16 to 28.)
 - The CIDR of a subnet must fall within the CIDR of the VPC, or is the same as the CIDR of the VPC.
 For example, if the IP range of the VPC is `192.168.0.0/16`, then the IP range of a subnet in the VPC can be `192.168.0.0/16` or `192.168.0.0/17`. 

![2](https://main.qcloudimg.com/raw/a2aab5034960c9cfb517b053d4107c0f.png)

## Deleting a VPC
>The prerequisites for deleting a VPC are that no IP addresses in the VPC are occupied and no resources (such as CVMs, TencentDBs, and gateways) are available in the VPC.

1. Log in to [VPC Console](https://console.cloud.tencent.com/vpc).
2. At the top of the list, select the region of the VPC to be deleted.
3. In the list, locate the row of the VPC to be deleted. Click **Delete** in the operation column and then confirm the operation.
![](https://main.qcloudimg.com/raw/51fd2b0b31022dbc47e08467e539a7fe.png)

## Assigning and Releasing IPv6 CIDR Blocks for a VPC
>Currently, the IPv6 EIP is in the beta test stage. If you do need to use it, please submit a Beta test application.

1. Log in to [VPC Console](https://console.cloud.tencent.com/vpc).
2. At the top of the "VPC" list, select **Region** to display the information of all VPC instances in the region.
3. In the operation column for the VPC for which IPv6 is to be enabled, click **Edit CIDR**.
4. In the window that appears, choose **Obtain** from the IPv6 CIDR drop-down list, and then click **OK**. The system will assign the `/56` IPv6 CIDR block to the VPC.
![](https://main.qcloudimg.com/raw/f8eb3a5d86ac47a3046575d2330cfd58.png)
4. For a VPC that has obtained an IPv6 CIDR block, you can click **Edit CIDR** in the operation column, and then click **Release** for IPv6 CIDR in the pop-up window to release the IPv6 address segment.

## Viewing All Resources in a VPC
1. Log in to [VPC Console](https://console.cloud.tencent.com/vpc).
2. At the top of the list, select the region of the VPC to be viewed, and click the ID of the VPC to be viewed in the list to go to the details page.
![1](https://main.qcloudimg.com/raw/2058cc7ea595f0c53d068c40d01493c4.png)
3. In the "Resources Included" column, you can view all the resources in the VPC.
![](https://main.qcloudimg.com/raw/31fdffbfa34db31772b2bc87d280ac0c.png)
