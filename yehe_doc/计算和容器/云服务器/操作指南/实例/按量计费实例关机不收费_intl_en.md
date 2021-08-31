## Overview
If you enable "No Charge when Shut Down" when shutting down a pay-as-you-go instance, the billing of CPU and memory resources of this instance stops. However the Cloud disks (system disk and data disk), public network bandwidth, images, and other key components of the CVM instance are still billed.
>! When this feature is enabled, the instance’s CPU and memory resources **will not be retained**, and the public IP address **will be automatically released** after shutdown. For more information about the feature, its use limits, and impacts, see [No Charges When Shut down for Pay-as-You-Go Instances](https://intl.cloud.tencent.com/document/product/213/19918).

## Directions
### Shutting down an instance via console
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm).
2. Choose the appropriate operation method based on your actual needs.
 - Shutting down a single instance:
    1. Select the instance you want to shut down, and click **More** > **Instance Status** > **Shut down** under the **Operation** column on the right.
    2. Tick **CVM No Charge when Shut down** and click **OK**.
    If the instance does not support this feature, **"No Charge when Shut Down" is not supported** will be displayed in the instance list.
 - Shutting down multiple instances:
    1. Select all the instances you want to shut down and click **Shut down** at the top of the list to shut down instances in batches.
    Reasons are given for instances that cannot be shut down.
	 2. Tick **CVM No Charge when Shut down** and click **OK**.
		If the instance does not support this feature, **"No Charge when Shut Down" is not supported** will be displayed in the instance list.

### Shutting down an instance via API
You can use the `StopInstances` API to shut down an instance. For details, please see [StopInstances](https://intl.cloud.tencent.com/document/product/213/33235). To enable this feature via API, please add the following parameter:

| Parameter Name | Required | Type | Description |
| ----------- | ---- | ------ | ------------------------------------------------------------ |
| StoppedMode | No   | String |The "No Charge when Shut down" feature is only available for pay-as-you-go instances.<br>**Valid values:**<br>KEEP_CHARGING: the instance incurs fees after shutdown<br>STOP_CHARGING: no charges when shut down<br>**Default value:**<br>KEEP_CHARGING |



