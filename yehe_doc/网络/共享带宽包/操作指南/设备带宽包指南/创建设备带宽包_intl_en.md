This document introduces how to create a device bandwidth package under your bill-by-CVM account.

>? 
>- BWP is currently in beta test. If you want to use it, please [submit an application](https://intl.cloud.tencent.com/apply/p/86ulv50u1e8).
>- A bill-by-CVM account only supports creating a device bandwidth package. For more information about your account type, see [Checking Account Type](https://intl.cloud.tencent.com/document/product/684/15246).

## Restrictions
1. Only one device bandwidth package can be enabled in a region.
2. After a device bandwidth package is created in a region, all CVMs and CLBs in the current region will be billed in the package, and no other billing mode is used in the region.
3. The original fees billed by monthly subscription will be refunded after being converted based on the number of hours actually used.

## Directions
1. Log in to the [Virtual Private Cloud Console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **Bandwidth Package** in the left sidebar.
3. Select a region, and click **+ New** in the upper-left corner.
4. In the **Create Bandwidth Package** pop-up window, enter the bandwidth package name, select a billing mode, and then click **Create**.
![](https://main.qcloudimg.com/raw/6aac805bcb27daeb1a6ac01fd07c6078.png)
5. After the bandwidth package is created, we recommend that you set a bandwidth cap for the resources in the bandwidth package to avoid high fees. For example, you can perform the following operations:
 - To set a bandwidth cap for a CVM:
    1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/instance/index?rid=1).
    2. On the **Instances** page, locate the CVM for which you want to set the bandwidth cap, choose **More** -> **Resource Adjustment**  -> **Adjust Network** under its **Operation** column.
    ![](https://main.qcloudimg.com/raw/1457ec84e27b2abb0c8b01cf214cc02c.png) 
 - To set a bandwidth cap for a CLB:
    1. Log in to the [Cloud Load Balancer Console](https://console.cloud.tencent.com/clb/index?rid=1&type=2%2C3).
    2. Locate the CLB for which you want to set the bandwidth cap, choose **More** -> **Adjust Bandwidth** under its **Operation** column..
