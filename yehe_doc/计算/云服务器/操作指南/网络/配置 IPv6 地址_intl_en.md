## Introduction
This article describes how to enable IPv6 support for you CVM.
> Currently EIPv6 is in beta now. Submit an application if you want to use it.
>


## Prerequisites

1. You need a [Tencent Cloud account](https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2F).
2. IPv6 is only supported in the following region: Beijing, Shanghai and Guangzhou.
3. Global Unicast Addresses (GUA) are used. Each VPC is assigned a `/56` CIDR block. Each subnet is assigned a `/64` and each ENI is assigned a single IPv6 address.
4. Both primary ENIs and secondary ENIs support IPv6 address. For more information, refer to [ENI documentation](https://intl.cloud.tencent.com/document/product/576).

## Directions
> Since IPv6 support is currently in beta, CVMs do not by default come with IPv6 addresses. If you want to use IPv6, you need to enable it manually.
> 

### Step 1: Purchasing a CVM (Optional)

> If you already have a CVM, skip this step.
> 
1. Log in to the [CVM purchase page](http://manage.qcloud.com/shoppingcart/shop.php?tab=cvm).
2. Select a region and VPC that supports IPv6 when picking a model.
3. Select a security group that supports IPv6 when configuring the CVM, and select **Assign free IPv6 address**.
4. Confirm your configuration and complete the purchase.

<span id="step2_configIPv6"></span>
### Step 2: Enabling IPv6 Support

Different operating systems have different instruction on enabling IPv6 support. For more information, please see the CVM configuration IPv6 document provided by VPC.
