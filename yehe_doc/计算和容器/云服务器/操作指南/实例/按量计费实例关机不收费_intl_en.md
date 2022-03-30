## Overview
The "No Charges when Shut Down" feature means eligible pay-as-you-go instances that have been **shut down** will not be billed for CPU and memory. Cloud disks (system disk and data disk), public network bandwidth, images, and other key components of the CVM instance are still billed.

<dx-alert infotype="notice" title="">
After this feature is enabled, the instance's CPU and memory **will no longer be retained**, and the public IP address **will be automatically released** after shutdown. For more information on this feature and its use limits and impact, see [No Charges When Shut Down for Pay-as-You Go Instances](https://intl.cloud.tencent.com/document/product/213/19918).
</dx-alert>



## Directions
<dx-tabs>
::: Shutting down instance in the console

#### Shutting down single instance
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm).
2. On the instance management page, proceed according to the actually used view mode:
  - **List view**: select the target instance and click **More** > **Instance Status** > **Shutdown** in the **Operation** column on the right as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/6bc11c552db35a4882506449573cf239.png)
   - **Tab view**: on the page of the target instance, click **Shutdown** in the top-right corner as shown below:
 ![](https://qcloudimg.tencent-cloud.cn/raw/8602dbbdc2f30d072fe53d62e40963e4.png)
3. Select **No charges when shut down** and click **OK**.
    If the instance does not support this feature, **"No Charges when Shut Down" is not supported** will be displayed in the instance list.



#### Shutting down multiple instances
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm).
2. Select all the instances you want to shut down and click **Shutdown** at the top of the list to batch shut down them as shown below:
Reasons are given for instances that cannot be shut down.
![](https://qcloudimg.tencent-cloud.cn/raw/7c3e7ab231472f3fe8fa8d0bdd7ff685.png)
2. Select **No charges when shut down** and click **OK**.
If the instance does not support this feature, **"No Charges when Shut Down" is not supported** will be displayed in the instance list.
:::
::: Shutting down instance via TencentCloud API
You can use the `StopInstances` API to shut down an instance. For details, please see [StopInstances](https://intl.cloud.tencent.com/document/product/213/33235). To enable this feature via API, please add the following parameter:

| Parameter Name | Required | Type | Description |
| ----------- | ---- | ------ | ------------------------------------------------------------ |
| StoppedMode | No   | String |The "No Charges when Shut down" feature is only available for pay-as-you-go instances.<br>**Valid values:**<br>KEEP_CHARGING: the instance incurs fees after shutdown<br>STOP_CHARGING: no charges when shut down<br>**Default value: **<br>KEEP_CHARGING |

:::
</dx-tabs>
