## Scenario
"CVM No Charge When Shut Down" means pay-as-you-go instances (CPUs and memory) that have been **shut down** will not be billed. Cloud disks (system disk and data disk), public network bandwidth, images, and other key components of the CVM are still billed. For more information, please see [No Charges When Shut down for Pay-as-You-Go Instances Details](https://intl.cloud.tencent.com/document/product/213/19918).

## Directions
### Shut down an instance via console
1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm).
2. Choose different operation methods based on actual needs.
 - Shutting down a single instance:
    1. Select the instance you want to shut down, and click **More** > **Instance Status** > **Shutdown** on the right operation column.
    2. Tick **CVM No Charge when Shut down** and click **OK**.
    If the instance does not support this feature, "No Charge when Shut Down" is not supported will be displayed in the instance list.
 - Shutting down multiple instances:
    1. Select all the instances you want to shut down and click **Shutdown** at the top of the list to shut down instances in batches.
    Reasons are given for instances that cannot be shut down.
	 2. Tick **CVM No Charge when Shut down** and click **OK**.
		If the instance does not support this feature, "No Charge when Shut Down" is not supported will be displayed in the instance list.

### Shut down an instance via API
You can use StopInstances API to shut down an instance. For details, please see [StopInstances](https://intl.cloud.tencent.com/document/product/213/15743). To enable this feature via API, please add the following parameter:

| Parameter Name | Required | Type | Description |
| ----------- | ---- | ------ | ------------------------------------------------------------ |
| StoppedMode | No   | String |The "No Charge when Shut down" feature is only available for pay-as-you-go instances<br>**Range:**<br>KEEP_CHARGING: Keep charging after the instance is shut down<br>STOP_CHARGING: No charge when shut down<br>**Default value:**<br>KEEP_CHARGING |
