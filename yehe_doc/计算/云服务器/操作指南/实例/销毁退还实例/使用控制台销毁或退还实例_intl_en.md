## Overview
This document describes how to terminate/return a pay-as-you-go CVM instance in the console.

<dx-alert infotype="notice" title="">
For the impact of terminating/returning a CVM instance, see [Impacts](https://intl.cloud.tencent.com/zh/document/product/213/4930#.E7.9B.B8.E5.85.B3.E5.BD.B1.E5.93.8D).
</dx-alert>





## Directions
### Terminating and releasing pay-as-you-go instances
For pay-as-you-go instances, you can choose immediate termination or timed termination.

1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/).
2. On the instance management page, proceed according to the actually used view mode:
  - **List view**: in the row of the target instance, select **More** > **Instance Status** > **Terminate/Return** on the right as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/726281e9ed830a1b88572d8cb4413c2c.png)
If you need to terminate multiple instances at the same time, select the instances and click **More Actions** > **Terminate/Return** at the top of the list.
  - **Tab view**: on the details page of the target instance, click **Terminate/Return** in the top-right corner of the page as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/adb8e0566baad43931ec61c17b2a3da8.png)
3. In the **Terminate/Return** pop-up window, choose **Immediate Termination** or **Timed Termination**.

 	 - **Immediate Termination**: if you choose immediate termination, you can choose whether to release resources now or 2 hours later. If you choose to release resources now, the instance data will be cleared and cannot be restored.
 	 - **Timed Termination**: if you choose timed termination, you need to specify the termination time. The instance will be terminated and released upon expiration, and the data cannot be restored.
4. After choose a termination option, click **Next** to confirm the actual resources to be terminated or retained.
5. After confirming the resources to be terminated, click **Start Termination**.
:::
</dx-tabs>




## Related Operations
### Canceling timed termination

1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/).
2. In the instance list, find the instance for which you want to cancel timed termination. In the "**Instance Billing Mode**" column, find "**Timed Termination**" and move the mouse cursor to <img src="https://main.qcloudimg.com/raw/2b612d7419315e76aaa9a7f3a7c9a447.png" style="margin: 0;"></img> to display the timed termination dialog box, as shown below:
![](https://main.qcloudimg.com/raw/2a57f29e939d794df1a25f41b0a4880a.png)
3. Click **Cancel**. A dialog box is displayed prompting you to confirm the cancellation.
4. In the dialog box, confirm the information of the instance for which you want to cancel timed termination and click **OK**. The cancellation takes effect immediately, as shown below:
![](https://main.qcloudimg.com/raw/4ee8b052dad3f348f726ba74956d95c5.png)

