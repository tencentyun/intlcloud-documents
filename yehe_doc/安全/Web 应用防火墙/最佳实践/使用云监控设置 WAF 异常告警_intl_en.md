This document describes how to configure alarms in the Cloud Monitor console to detect WAF instance exceptions.

## Prerequisites
- You have activated [WAF](https://intl.cloud.tencent.com/pricing/waf).
- You have configured the [domain name list](https://intl.cloud.tencent.com/document/product/627/47531).

## Directions
### Step 1. Configure the trigger condition template[](id:CFTJ)
1. Log in to the [Cloud Monitor console](https://console.cloud.tencent.com/monitor/overview) and select **Alarm Management** > **Trigger Condition Template** on the left sidebar.
2. On the **Trigger Condition Template** page, click **Create**.
3. In the pop-up window, complete all the settings and click **Save**.

Parameters:
 - **Template Name**: Enter a template name.
 - **Remarks**: Enter template remarks.
 - **Policy type**: Select **WAF**.
 - **Apply preset trigger conditions**: Select this option to enable preset trigger conditions for the corresponding monitored service.
 - **Trigger condition**:
    - It supports metric alarm and event alarm. Click **Add** to set multiple alarms.
    - WAF can monitor a range of conditions, including the number of accesses, number of web attacks, number of CC attacks, upstream and downstream bandwidth, QPS, number of bot attacks, percentage of web attacks, percentage of bot attacks, and percentage of CC attacks.

### Step 2. Configure the notification template[](id:TZMB)
1. Log in to the [Cloud Monitor console](https://console.cloud.tencent.com/monitor/overview) and select **Alarm Management** > **Notification Template** on the left sidebar.
2. On the **Notification Template** page, click **Create**.
3. On the pop-up page, complete all the settings and click **Complete**.

Parameters:
 - **Template Name**: Enter a custom template name.
 - **Notification Type**:
    - Alarm Trigger: A notification will be sent when an alarm is triggered.
    - Alarm Recovery: A notification will be sent when an alarm is resolved.
 - **Language**: Select Chinese or English.
 - **User Notification**:
    - Recipient Object: Select a recipient group or recipient.
    - Notification Period: Define the time period for receiving alarms.
    - Receiving Channel: Email, SMS, WeChat, or phone call.
 - API Callback: You can enter up to three URLs accessible over the public network as the callback API addresses, and Cloud Monitor will push alarm messages to them promptly. If the HTTP response returns code 200, the verification is successful. For more information on alarm callback fields, see [Alarm Callback](https://intl.cloud.tencent.com/document/product/248/38919). 
 - Deliver to CLS: After it is enabled, alarms will be delivered to specific log topics of CLS in real time.

### Step 3. Configure the alarm policy
1. Log in to the [Cloud Monitor console](https://console.cloud.tencent.com/monitor/overview) and select **Alarm Configuration** > **Alarm Policy** on the left sidebar.
>?You can add, modify, and copy an alarm policy, and view the alarm history of the policy on the alarm policy page. Each policy can be associated with the configured [trigger condition](#CFTJ) and [notification template](#TZMB).
2. On the **Alarm Policy** page, click **Create**.
3. Perform the following steps:
   1. **Basic Info**: Enter the basic information including the name and remarks, and select WAF as the policy type.
2. **Alarm Object**: Select a WAF instance as the object. To select an instance group as the object, you need to create groups manually.

>?
>- Instance ID: The alarm policy is associated with the selected instance.
>- Instance Group: The alarm policy is associated with the selected instance group.
>- All Objects: The alarm policy is associated with all instances the current account has permission on.



   3. **Trigger Condition**: Select the [trigger condition template](#CFTJ) you set or configure it manually.

   4. **Notification Template**: Select the just configured [notification template](#TZMB) and click **Confirm** to save it.

   5. **Advanced Configuration (Optional)**: Click ![](https://main.qcloudimg.com/raw/ad0958699f9a6b2f6a153205fb865a22.png) to enable auto scaling. The auto scaling policy will be triggered if the alarm condition is met.

   6. After following the instructions above, click **Complete**.
