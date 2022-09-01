## Overview
DTS can use EventBridge to monitor events during data migration, sync, and subscription tasks and set alarm rules. EventBridge will send notifications to you as soon as an event is triggered, so you can take corresponding measures. 

This document describes how to set notification rules for event alarms, including the scope of event alarms, form of notifications, time period for notifications, and recipient group. 

## Directions
1. Log in to the [EventBridge console](https://console.cloud.tencent.com/eb).
2. The system will ask you to authorize the service as instructed in [Activating EventBridge](https://intl.cloud.tencent.com/document/product/1108/42272) when you log in for the first time. If you have already authorized it, skip this step.
3. Select **Event rule** on the left sidebar, select the **Guangzhou** region and **Default** event bus, and click **Create event rule**.
As the event buses of Tencent Cloud services are uniformly stored in Guangzhou by default, you cannot select other options for the region and event bus here.
![](https://qcloudimg.tencent-cloud.cn/raw/01bd03e8bdad4b11276e2a8fdfa516a9.png)
4. Configure the event rule and click **Next**.
 - **NewDTS (data migration/sync/subscription (Kafka Edition))**
    ![](https://qcloudimg.tencent-cloud.cn/raw/5feb1408d29bc9c825423fd77449a30d.png)
 - **Old DTS (data subscription only)**
    ![](https://qcloudimg.tencent-cloud.cn/raw/29819a0c4d5a00137927c171c49ab374.png)
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Rule name</td>
<td>Enter a rule name to distinguish between services, which cannot be modified once configured.</td></tr>
<tr>
<td>Rule pattern</td>
<td>Select <strong>Default</strong>. </td></tr>
<tr>
<td>Tencent Cloud service</td>
<td><ul><li>For NewDTS tasks (migration/sync/subscription (Kafka Edition)), select <strong>Data Transmission Service (DTS)</strong>. </li><li>For old DTS tasks (subscription only), select <strong>DTS data subscriptions</strong>.</li></ul></td></tr>
<tr>
<td>Event type</td>
<td><ul><li>For NewDTS tasks (migration/sync/subscription (Kafka Edition)), select <strong>Data migration task interrupted</strong>, <strong>Data synchronization task interrupted</strong>, and <strong>Data subscription task interrupted</strong>. </li><li>For old DTS tasks (subscription only), <strong>All events</strong> is selected by default.</li></ul></td></tr>
</tbody></table>
5. Configure the notification method, recipient, and delivery method, select **Notification message** for **Trigger method**, and click **Complete**.
To add a new recipient user or user group, go to the [CAM](https://console.cloud.tencent.com/cam) console for creation and then select it in **Recipients** in this step.
To configure different trigger methods, click **Add** at the bottom to add more delivery targets.
6. Return to the event rule list and confirm that the created event rule has been enabled. Subsequently, when a task exception triggers an alarm, the configured recipients will receive message notifications.
![](https://qcloudimg.tencent-cloud.cn/raw/cda96cd6cc44dbd7c139bab1a13e0972.png)

