As shown on the right of the following figure, the basic network is a public network resource pool for all users on Tencent Cloud. The private IP addresses of all CVMs are centrally assigned by Tencent Cloud, which means IP range division and IP addresses cannot be customized.
VPC refers to a logically isolated network space built by the user on Tencent Cloud, as shown on the left of the following figure. In a VPC, you can customize IP ranges, IP addresses, and routing policies. Compared with the basic network, VPC instances are more suitable for scenarios in which network configurations need to be customized.
![](https://main.qcloudimg.com/raw/13072e70d41994799c310bb033cdda25.png)
>
>1. As basic network resources are becoming increasingly sparse and cannot be expanded, the basic network is no longer supported by accounts that were registered after June 13, 2017. This means that instances (such as CVMs and CLBs) cannot be created in the basic network, with support only provided for VPC instances.
>2. You can query the network attributes of an account through the DescribeAccountVpcAttributes API.
>3. To use basic network services, submit an application.

## Migrating CVMs from a Basic Network to a VPC
To facilitate the use of VPC instances, Tencent Cloud provides you with the service of migrating a single CVM or a batch of CVMs from the basic network to a VPC. For the operation procedure, see [Switching to a VPC](https://intl.cloud.tencent.com/document/product/213/20278).

>Classiclink only supports VPC instances with the IP range of 10.0-47.0/16 (including its subsets). If the IP range of your VPC is out of this range, you will be unable to interconnect with basic network CVMs.
## Associating a Basic Network CVM with VPC
Classiclink can be used to make the CVM "TomCVM" communicate with the VPC "TomVPC". The detailed steps are as follows:
1. Log in to [VPC Console](https://console.cloud.tencent.com/vpc).
2. Select the region as Guangzhou, and click the ID of `TomVPC` that is to be interconnected with the basic network to go to the details page.
3. Click the **Classiclink** tab, and then click **+Associate CVM**. 
4. In the window that appears, select the CVM in the basic network to be associated with the VPC `TomCVM`. Then, click **OK**.

## Viewing CVMs interconnected with the Basic Network
1. Log in to [VPC Console](https://console.cloud.tencent.com/vpc).
2. Select the region and click the ID of the VPC to be interconnected with the basic network to go to the details page.
3. Click the **Classiclink** tab to view the list of basic network CVMs associated with the VPC.


## Disassociating a VPC from the CVMs of a Basic Network<span id="release">
1. Log in to [VPC Console](https://console.cloud.tencent.com/vpc).
2. Click the ID of the VPC to be interconnected with the basic network to go to the details page.
3. Click the **Classiclink** tab, select the CVM to be disassociated from the list of basic network CVMs, click **Disassociate** in the operation column, and confirm the operation.


