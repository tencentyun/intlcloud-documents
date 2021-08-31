This document describes how to create a device bandwidth package under your bill-by-CVM account.

>?BWP is currently in beta. To try it out, please submit an application to be added to the beta list.
>

## Restrictions
- Only a bill-by-CVM account can create a device bandwidth package. You can check your account type as instructed in [Checking Account Type](https://intl.cloud.tencent.com/document/product/684/15246).
- Only one device bandwidth package can be activated in a region.
- After a device bandwidth package is created in a region, all CVMs and CLBs in the region will be automatically billed in the bandwidth package, and no other billing mode is used in the region. The original fees billed by monthly subscription will be refunded after being converted based on the number of hours actually used.

## Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1) and click **Bandwidth Package** on the left sidebar.
2. Select a region, and click **+New** in the upper-left corner.
3. In the pop-up window, enter the bandwidth package name, select a billing mode, and then click **Create**.

4. (Optional) After the bandwidth package is created, we recommend that you set a bandwidth cap for the following resources:
 - Set a bandwidth cap for CVM instances as instructed in [Adjusting Network Configuration](https://intl.cloud.tencent.com/document/product/213/15517).
 - Set a bandwidth cap for CLB instances as instructed in [Adjusting Public Network Configuration](https://intl.cloud.tencent.com/document/product/214/39528).
