## Overview
This article describes how to set up a CVM instance with an IPv6 CIDR block and enable IPv6 for your ENI to implement communications across the internet and intranet.


<dx-alert infotype="explain" title="">
Currently, Elastic IPv6, IPv6 CLB, and IPv6 VPC are only available in the following regions: Guangzhou, Shenzhen Finance, Shanghai, Shanghai Finance, Nanjing, Beijing, Chengdu, Hong Kong (China), Singapore, and Virginia. If you need to use the services in other regions, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category).
</dx-alert>




## Prerequisites

1. You need a [Tencent Cloud account](https://intl.cloud.tencent.com/register?&s_url=https%3A%2F%2Fconsole.intl.cloud.tencent.com%2Fworkorder%2Fcategory).
2. Currently, Elastic IPv6, IPv6 CLB, and IPv6 VPC are only available in the following regions:
Guangzhou, Shenzhen Finance, Shanghai, Shanghai Finance, Nanjing, Beijing, Chengdu, Hong Kong (China), Singapore, and Virginia. If you need to use the services in other regions, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category).
3. Global Unicast Addresses (GUA) are used. Each VPC is assigned a `/56` CIDR block. Each subnet is assigned a `/64` and each ENI is assigned a single IPv6 address.
4. Both primary ENIs and secondary ENIs support IPv6 address. For more information, refer to [ENI documentation](https://intl.cloud.tencent.com/zh/document/product/576).
5. Cloud Physical Machine (CPM) 2.0 does not support the feature of configuring IPv6 addresses during instance creation. If you need to use the feature, enable it on the **IP and ENI > Elastic IPv6** page in the VPC console after creating the CPM 2.0 instance.
## Directions


<dx-alert infotype="explain" title="">
Since IPv6 support is currently in beta, CVM instances do not come with IPv6 addresses by default. If you want to use IPv6, you need to enable it manually.
</dx-alert>



### Step 1: Purchasing a CVM (Optional)



<dx-alert infotype="explain" title="">
If you already have a CVM, skip this step.
</dx-alert>


1. Log in to the [CVM purchase page](http://manage.qcloud.com/shoppingcart/shop.php?tab=cvm&_ga=1.87370846.770173325.1571651505).
2. Select a region and VPC that supports IPv6 when picking a model.
3. Select a security group that supports IPv6 when configuring the CVM, and select **Assign free IPv6 address**.
<dx-alert infotype="notice" title="">
If the VPC or security group you selected does not support IPv6, create a VPC or security group that supports IPv6 for the instance by referring to "Setting up IPv6 VPCs" after the instance is created.
</dx-alert>
4. Confirm your configuration and complete the purchase.

