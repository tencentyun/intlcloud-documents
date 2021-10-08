This document describes how to set alarms in the cloud monitoring platform when a Web Application Firewall (WAF) instance is exceptional.

## Prerequisites
You have activated [Web Application Firewall](https://buy.cloud.tencent.com/buy/waf).

## Directions
### Step 1. Configure the trigger condition template[](id:CFTJ)
1. Log in to the [Cloud Monitor Console](https://console.cloud.tencent.com/monitor/overview), and select **Alarm Management** > **Trigger Condition Template** on the left sidebar.
2. On the trigger condition template page, click **Create**.
3. In the pop-up window, complete all the settings and click **Save**.
>?
>- **Template Name**: enter a template name.
>- **Remarks**: enter template remarks.
>- **Policy Type**: select WAF.
>- **Use preset trigger conditions**: select this option to enable preset trigger conditions for the corresponding monitored service.
>- **Trigger Condition**:
>  - It supports metric alarm and event alarm. Click **Add** to set multiple alarms.
>  - WAF can monitor a range of conditions, including the number of accesses, number of web attacks, number of CC attacks, upstream and downstream bandwidth, QPS, number of bot attacks, percentage of web attacks, percentage of bot attacks, and percentage of CC attacks.




### Step 2. Configure the notification template[](id:TZMB)
1. Log in to the [Cloud Monitor Console](https://console.cloud.tencent.com/monitor/overview), and select **Alarm Management** > **Notification Template** on the left sidebar.
2. On the notification template page, click **Create**.
3. On the pop-up page, complete all the settings and click **Complete**.
>?
> - **Template Name**: enter a custom template name.
> **Notification Type**：
>  - Alarm trigger: a notification will be sent when an alarm is triggered.
>  - Alarm recovery: a notification will be sent when an alarm is recovered.
> - **Language**: select a language from Chinese and English.
> - **User Notification**:
>  - Recipient object: select a recipient group or recipient.
>  - Notification time: set a time period for receiving alarm notifications.
>  - Receiving channel: email, SMS, and phone calls.
>- **API Callback**: enter a URL that is accessible over the public network. You can enter up to three ones. This address will receive an alarm message from Cloud Monitor promptly. If it receives an HTTP code 200, the verification is successful. For more details on alarm callback fields, see [Alarm Callback](https://intl.cloud.tencent.com/document/product/248/38919).



### Step 3. Configure the alarm policy
1. Log in to the [Cloud Monitor Console](https://console.cloud.tencent.com/monitor/overview) console and select **Alarm Configuration** > **Alarm Policy** on the left sidebar.
>?You can add, modify and copy an alarm policy, and view the alarm history of the policy on the alarm policy page. Each policy can be associated with the configured [trigger condition](#CFTJ) and [notification template](#TZMB).
2. On the alarm policy page, click **Create**.
3. Perform the following steps:
   i. **Basic Info**: fill in the basic information including the name and remark, and select WAF as the policy type.
   
   ii. **Alarm Object**: select a WAF instance as the object. To select an instance group as the object, you need to create groups manually.

>?
>- If you select "Instance ID", the alarm policy is associated with the selected instance.
>- If you select "Instance Group", the alarm policy is associated with the selected instance group.
>- If you select "All Objects", the alarm policy is associated with all instances the current account has permission on.

​     iii. **Trigger Condition**: select the [trigger condition template](#CFTJ) you set or configure it manually.

​     iv. **Notification Template**: select the [notification template](#TZMB) you set, and click **Confirm** to save it.

​     v. **Advanced Configuration (Optional)**: click ![](https://main.qcloudimg.com/raw/ad0958699f9a6b2f6a153205fb865a22.png) to enable auto scaling. The auto scaling policy will be triggered if the alarm condition is met.
4. After following the instructions above, click **Complete**.

