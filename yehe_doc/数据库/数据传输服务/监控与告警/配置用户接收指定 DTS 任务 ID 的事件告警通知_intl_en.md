## Overview

This document describe how to receive only the event alarm notifications of tasks with specified IDs after you create migration, sync, or subscription tasks.

## Directions

1. Log in to the [EventBridge console](https://console.cloud.tencent.com/eb).
2. The system will ask you to authorize the service as instructed in [Activating EventBridge](https://intl.cloud.tencent.com/document/product/1108/42272) when you log in for the first time. If you have already authorized it, skip this step.
3. Select **Event rule** on the left sidebar, select the **Guangzhou** region and **Default** event bus, and click **Create event rule**.
As the event buses of Tencent Cloud services are uniformly stored in Guangzhou by default, you cannot select other options for the region and event bus here.
![](https://qcloudimg.tencent-cloud.cn/raw/01bd03e8bdad4b11276e2a8fdfa516a9.png)
4. Configure the event rule and click **Next**.
  - Rule name: Enter a rule name to distinguish between services, which cannot be modified once configured.
  - Rule pattern: Select **Custom events**.
  - Rule pattern preview: Copy the following sample code and replace the sample task ID with the actual ID of the DTS task to be monitored. You can separate multiple tasks by comma.
<img src="https://qcloudimg.tencent-cloud.cn/raw/29819a0c4d5a00137927c171c49ab374.png" style="zoom:90%;" />
```
// Example of receiving notifications for a single task ID
    {
     "source":"dts.cloud.tencent",
     "subject":"sync-jt12XXgt"
    }
		
// Example of receiving notifications for multiple task IDs
    {
     "source":"dts.cloud.tencent",
     "subject":["sync-jt12XXgt","dts-a5uqXXhs"]
    }
```
Sample task ID in the DTS console:
<img src="https://qcloudimg.tencent-cloud.cn/raw/8f12fc6a4c272e676b1642b439190def.png" >

5. Configure the notification method, recipient, and delivery method, select **Notification message** for **Trigger method**, and click **Complete**.
To add a new recipient user or user group, go to the [CAM](https://console.cloud.tencent.com/cam) console for creation and then select it in **Recipients** in this step.
To configure different trigger methods, click **Add** at the bottom to add more delivery targets.

6. Return to the event rule list and confirm that the created event rule has been enabled. Subsequently, when a task exception triggers an alarm, the configured recipients will receive message notifications.
![](https://qcloudimg.tencent-cloud.cn/raw/cda96cd6cc44dbd7c139bab1a13e0972.png)
