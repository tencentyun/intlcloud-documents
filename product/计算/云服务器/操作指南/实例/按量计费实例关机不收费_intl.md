With "No Charges When Shut Down" enabled, users don't need to pay for Pay-as-you-go instances (CPUs, memory) that are **shut down** by themselves. However other resources bound with these instances, like cloud disks (system disk, data disk), public network bandwidth and images, are still charged. For more information, please see [Instruction of No Charged When Shut Down for the Pay as You Go Instances](https://cloud.tencent.com/document/product/213/19918 ).

## Enabling on Console 
1. Log into [CVM Console](https://console.cloud.tencent.com/cvm).
2. Shut down one instance: Select an instance and click **Shutdown** on the top of the list. Or in the **Operation**, select **More > Instance Status > Shutdown**. Check **No charges when shut down** in the pop-up page. **Does not support No charges when shut down** will be displayed if the instance is not available for this feature.
3. Shut down several instances: Select desired instances and click **Shutdown** on the top of the list. Check **No charges when shut down**. **Does not support No charges when shut down** will be displayed if the instance is not available for this feature.

![](https://main.qcloudimg.com/raw/bd3e5bd060565ca74b24a9a898feb13d.png)
## Enabling via Cloud API 
To enable this feature via API, please add the following parameter while shutting down instance using StopInstances API. For details, please see [StopInstances](https://cloud.tencent.com/document/product/213/15743). 

| Parameter Name    | Required | Type   | Description                                                         |
| ----------- | ---- | ------ | ------------------------------------------------------------ |
| StoppedMode | No   | String | Feature No charges when shut down is only available for Pay as you go Cloud Disk<br>**Range：**<br>KEEP_CHARGING：Keep charging when shut down<br>STOP_CHARGING：No charges when shut down<br>**Default value：**<br>KEEP_CHARGING |
