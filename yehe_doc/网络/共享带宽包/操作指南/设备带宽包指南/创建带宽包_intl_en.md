>? BWP is currently in beta test. If you want to try it out, please [submit an application](https://intl.cloud.tencent.com/apply/p/86ulv50u1e8).

## Restrictions
1. Only one device bandwidth package can be activated in each region.
2. After a device bandwidth package is activated in a region, all CVMs and CLBs in the current region are automatically billed by bandwidth package. The bandwidth package cannot be used together with any other billing mode in the same region.
3. The original fees billed by monthly subscription will be refunded after conversion based on the number of hours actually used.
4. To use IP bandwidth packages, bandwidth package users can [submit a ticket](https://console.cloud.tencent.com/workorder/category) to change the account type to bill-by-IP.

## Directions
1. Log in to the [Virtual Private Cloud Console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **Bandwidth Package** in the left sidebar.
3. Select a region, and click **+ New** at the top left.
4. In the pop-up window, enter a name, select a billing mode, and click **OK**.
![](https://main.qcloudimg.com/raw/6aac805bcb27daeb1a6ac01fd07c6078.png)
5. After the bandwidth package is created, we recommend that you set a bandwidth cap for the resources in the bandwidth package. For example, you can perform the following operations:
 - To set a bandwidth cap for CVM:
    1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/instance/index?rid=1).
    2. On the Instances page, choose **More** -> **Resource Adjustment** -> **Adjust Network** in the **Operation** column to set the bandwidth cap.
    ![](https://main.qcloudimg.com/raw/1457ec84e27b2abb0c8b01cf214cc02c.png)
 - To set a bandwidth cap for CLB:
    1. Log in to the [Cloud Load Balancer Console](https://console.cloud.tencent.com/clb/index?rid=1&type=2%2C3).
    2. In the **Operation** column, choose **More** -> **Adjust Bandwidth** to set the bandwidth cap.
