This article describes how to terminate and release a Cloud Virtual Machine (CVM) instance. For more information on expiration, see [Expiration Notifications](https://intl.cloud.tencent.com/document/product/213/2181).

## Overview

If you no longer need an instance, you can terminate it. The terminated instance is moved to the Recycle Bin. You can renew, restore, or release the instances in the Recycle Bin.

>! If your account is overdue, you need to add funds before restoring pay-as-you-go instances.
>

You can use the following methods to terminate and release pay-as-you-go instances:
 - **Manual termination:** if your account is in good standing, you can manually terminate a pay-as-you-go instance. A pay-as-you-go instance is released after it remains in the recycle bin for over 2 hours.
 - **Scheduled termination:** you can schedule a time (to the second) to automatically terminate a pay-as-you-go instance. You can select a future time to terminate resources. An instance terminated using scheduled termination bypasses the recycle bin and is released immediately. You can [cancel a scheduled termination](https://intl.cloud.tencent.com/document/product/213/4930) at any time before the scheduled time.
 - **Automatic termination upon expiration or when account is overdue**: a pay-as-you-go instance with its balance below 0 will be automatically released after 2 hours and 15days. For the first 2 hours, billing continues and you can still use the instance. For the next 15 days, however, the instance will be shut down, and billing will stop. Pay-as-you-go instances cannot be moved to the recycle bin after your account is overdue. Instead, you need to check the instance in the CVM instance list. You can continue to use the instance if you [renew it](https://intl.cloud.tencent.com/document/product/213/6143) within the specified time.

|  | Manual termination (not overdue) | Scheduled termination (not overdue) | Automatic termination upon expiration or when account is overdue |
|---------|---------|---------|---------|
| Pay-as-you-go instances | After termination, pay-as-you-go instances will be released after being retained in the recycle bin for a maximum of 2 hours. |Instances for which timed termination is set will be released immediately as scheduled, instead of going into the recycle bin. | When your account is overdue, for the first 2 hours, billing continues and you can still use the instance. For the next 15 days, however, the instance will be shut down, and billing will stop. Pay-as-you-go instances are not moved to the recycle bin after your account is overdue. If the instance is not renewed within this period, the instance will be released.|



## Impacts
What happen to the data, EIPs and charges of an instance once it is terminated:
- **Billing**: once an instance is terminated or released, no more charge will be incurred.
- **Instance data:** local disks and non-elastic cloud disks mounted to the instance are all released, and the data on these disks is lost. Back up the data in advance. Elastic cloud disks follow their own lifecycle.
- **EIP:** EIPs (including IP addresses on secondary ENIs) of a terminated instance are retained, and idle IP addresses may incur charges. If you don’t need them anymore, release them as soon as possible.



## Terminating and Releasing Pay-As-You-Go Instances

For pay-as-you-go instances, you can choose immediate termination or scheduled termination.

### Terminating instances using the Console

1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/).
2. Choose one of the following:
    - **Terminate a single instance**: find the desired instance in the list and click **More** -> **Instance Status** -> **Terminate/Return** on the right side.
    - **Terminate instances in batches**: select all desired instances and click **More** -> **Terminate/Return** on the top of the interface. For instances that cannot be terminated, the reasons will be displayed.
3. In the pop-up window, choose **Immediate Termination** or **Scheduled Termination**.
 	 - **Immediate Termination**: you can choose to release resources immediately or in 2 hours. If you choose to release resources immediately, the instance data is cleared and cannot be restored.
 	 - **Scheduled Termination**: if you choose scheduled termination, you need to specify the termination time. The instance is terminated and released at that time and the data cannot be restored.
4. Click **Next** to confirm the resources to be terminated or retained.
5. Click **Start Termination**.

### Canceling a scheduled termination

1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/).
2. In the instance list, find the desired instance and the corresponding **Scheduled Termination** in the **Instance Billing Plan** column. Move your cursor over <img src="https://main.qcloudimg.com/raw/2b612d7419315e76aaa9a7f3a7c9a447.png" style="margin: 0;"></img> to display the scheduled termination dialog box, as shown below:
![](https://main.qcloudimg.com/raw/2a57f29e939d794df1a25f41b0a4880a.png)
3. Click **Cancel**. A dialog box is displayed prompting you to confirm the cancellation.
4. In the dialog box, confirm the information of the instance for which you want to cancel timed termination and click **OK**. The cancellation takes effect immediately, as shown below:
![](https://main.qcloudimg.com/raw/4ee8b052dad3f348f726ba74956d95c5.png)

## Terminating Instances Using Tencent Cloud APIs

Refer to [TerminateInstances API](https://intl.cloud.tencent.com/document/product/213/33234) for more information.
