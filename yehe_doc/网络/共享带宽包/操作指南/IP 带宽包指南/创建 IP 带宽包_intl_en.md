This document introduces how to create an IP bandwidth package under your bill-by-EIP/CLB account.
>? 
>- BWP is currently in beta test. If you want to use it, please [submit an application](https://intl.cloud.tencent.com/apply/p/86ulv50u1e8).
>- A bill-by-EIP/CLB account only supports creating an IP bandwidth package. For more information about your account type, see [Checking Account Type](https://intl.cloud.tencent.com/document/product/684/15246).
>- If you have a bill-by-CVM account and want to use IP bandwidth packages, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) to change to bill-by-EIP/CLB account.

1. Log in to the [Virtual Private Cloud Console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **Bandwidth Package** in the left sidebar.
3. Select a region, and click **+ New** in the upper-left corner.
4. In the **Create Bandwidth Package** pop-up window, enter the bandwidth package name, select a billing mode, and then click **Create**.
![](https://main.qcloudimg.com/raw/6aac805bcb27daeb1a6ac01fd07c6078.png)
5. After the bandwidth package is created, we recommend that you set a bandwidth cap for the resources in the bandwidth package to avoid high fees. For example, you can perform the following operations:
 - To set a bandwidth cap for an EIP:
    1. Log in to the [EIP Console](https://console.cloud.tencent.com/cvm/eip).
    2. Locate the EIP for which you want to set the bandwidth cap, choose **More** -> **Adjustment network** under its **Operation** column.
    
 - To set a bandwidth cap for a CLB:
    1. Log in to the [Cloud Load Balancer Console](https://console.cloud.tencent.com/clb/index?rid=1&type=2%2C3).
    2. Locate the CLB for which you want to set the bandwidth cap, choose **More** -> **Adjust Bandwidth** under its **Operation** column.
		
		
