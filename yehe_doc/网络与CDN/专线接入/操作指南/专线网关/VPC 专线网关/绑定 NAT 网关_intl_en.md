If you have created a direct connect gateway and your business needs to access the public network through a NAT Gateway, you need to bind the direct connect gateway to the NAT Gateway. This document describes how to bind the direct connect gateway to a NAT Gateway.

## Prerequisite
- You have [created a VPC](https://intl.cloud.tencent.com/document/product/215/31805).
- You have [created a VPC-based direct connect gateway](https://intl.cloud.tencent.com/document/product/216/19256).
- You have [created a NAT Gateway](https://intl.cloud.tencent.com/document/product/1015/30251).

## Binding to a NAT Gateway
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. In the left sidebar, click **Direct Connect Gateway** to go to the management page.
3. In the list of direct connect gateways, click the name of the direct connect gateway that needs to be bound to a NAT Gateway to open the details page.
4. Select the desired NAT Gateway on the **Basic Information** page.
![]()

## Unbinding from a NAT Gateway
If you do not need the NAT Gateway to which the direct connect gateway is bound, you can go to the **Basic Information** tab on the direct connect gateway details page to unbind the direct connect gateway from it.
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. In the left sidebar, click **Direct Connect Gateway** to go to the management page.
3. In the list of direct connect gateways, click the name of the direct connect gateway that needs to be unbound from the NAT Gateway to open the details page.
4. On the **Basic Information** page, click **Unbind** in the row of **Bound NAT Gateway**, and click **OK** in the pop-up dialogue box.
![]()
