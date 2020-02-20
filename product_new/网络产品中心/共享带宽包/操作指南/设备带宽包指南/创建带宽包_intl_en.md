## Restrictions
1. Only one device bandwidth package can be enabled in a region.
2. After the device bandwidth package is created in a region, all CVMs and CLBs in the current region are changed to billing by bandwidth package, and no other billing method is used in the region.
3. The original monthly subscription fee will be refunded after being converted based on the number of hours actually used.
4. To use IP bandwidth packages, device bandwidth package users can [submit a ticket](https://console.cloud.tencent.com/workorder/category) to change the account type to “bill by traffic on IP”.

## Directions
1. Log in to the [Virtual Private Cloud Console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **Bandwidth Package** on the left sidebar.
3. Select a region, and click **+ New** in the upper-left corner.
4. In the pop-up window, enter a name, select a billing mode, and click **OK**.
5. After the bandwidth package is created, we recommend that you set a bandwidth cap for the resources in the bandwidth package. For example, you can perform the following operations:
 - To set a bandwidth cap for CVM:
    1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/instance/index?rid=1).
    2. On the Instances page, choose **More** -> **Resource Adjustment** -> **Adjust Network** in the Operation column to set the bandwidth cap. 
 - To set a bandwidth cap for CLB: 
    1. Log in to the [Cloud Load Balancer Console](https://console.cloud.tencent.com/clb/index?rid=1&type=2%2C3).
    2. In the Operation column, choose **More** -> **Adjust Bandwidth** to set the bandwidth cap.
