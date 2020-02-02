## Scenario

When users enable the  "No Charges When Shut down" feature, they will not need to pay for Pay-as-You-Go instances (CPUs, memory) that are in **shutdown** mode. However other resources bound with these instances, like cloud disks (system disk, data disk), public network bandwidth and images, are still charged. For more information, please see [No Charges When Shut down for Pay-as-You-Go Instances Details](https://intl.cloud.tencent.com/document/product/213/19918 ).

## Directions
1. Log into [CVM Console](https://console.cloud.tencent.com/cvm).
2. Shut down one instance: Select an instance and click **Shutdown** on the top of the list. Alternatively, go to the operation pane on the right, select **More > Instance Status > Shut down**. Check **No Charges when Shut down** in the pop-up page. **Does not support No Charges when Shut down** will be displayed if the instance is not eligible for this feature.
3. Shut down several instances: Select desired instances and click **Shut down** on the top of the list. Check **No Charges when Shut down**. **Does not support No Charges when Shut down** will be displayed if the instance is not eligible for this feature.

## Enabling via Cloud API 
To enable this feature via API, please add the following parameter while shutting down instance using StopInstances API. For details, please see [Stop Instances](https://intl.cloud.tencent.com/document/product/213/15743). 

| Parameter Name    | Required | Type   | Description                                                         |
| ----------- | ---- | ------ | ------------------------------------------------------------ |
| StoppedMode | No   | String | The "No Charges when Shut down" feature is only available for Pay-as-You-Go instances<br>**Range：**<br>KEEP_CHARGING：Keep charging when shut down<br>STOP_CHARGING：No charges when shut down<br>**Default value：**<br>KEEP_CHARGING |
