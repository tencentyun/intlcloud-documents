## Overview

Tencent Cloud provides the Cloud Monitor service for all users by default; therefore, you do not need to manually activate it. Cloud Monitor will start collecting monitoring data only after a Tencent Cloud product is used.

TDMQ for CMQ allows you to monitor the resources (topics and queues) created under your account, so that you can keep track of the status of your resources in real time. You can configure alarm rules for monitoring metrics. When a monitoring metric reaches the set alarm threshold, Cloud Monitor will notify you of exceptions in time via email, SMS, WeChat, phone call, etc.

## Directions

### Configuring alarm policy

An alarm policy can determine whether an alarm notification should be sent based on the comparison between the monitoring metric and the given threshold in the selected time period. You can promptly take appropriate precautionary or remedial measures when the alarm is triggered by a TDMQ for CMQ status change. Properly configured alarm policies help improve the robustness and reliability of your applications.

>!Be sure to configure alarms for your instance to prevent exceptions caused by traffic spikes or specification limits.

1. Log in to the [CM console](https://console.cloud.tencent.com/monitor).
2. On the left sidebar, select **Alarm Configuration** > **Alarm Policy** and click **Create**.
3. On the **Alarm Policy** page, select a policy type and instance and set the alarm rule and notification template.
	 - **Monitoring Type**: select **Cloud Product Monitoring**.
	 - **Policy Type**: select **TDMQ alarm** > **CMQ**.
	 - **Alarm Object**: select the TDMQ for CMQ resource for which to configure the alarm policy.
	 - **Trigger Condition**: you can select **Select template** or **Configure manually**. The latter is selected by default. For more information on manual configuration, see the description below. For more information on how to create a template, see [Creating trigger condition template](#Creating-trigger-condition-template).
>- Metric: for example, if you select 1 minute as the statistical period for the "message retention volume" metric, then if the message retention volume exceeds the threshold for N consecutive data points, an alarm will be triggered.
>- Alarm Frequency: for example, "Alarm once every 30 minutes" means that there will be only one alarm triggered every 30 minutes if a metric exceeds the threshold in several consecutive statistical periods. Another alarm will be triggered only if the metric exceeds the threshold again in the next 30 minutes.

  - **Notification Template**: you can select an existing notification template or create one to set the alarm recipient objects and receiving channels.
4. Click **Complete**.

For more information on alarms, see [Creating Alarm Policy](https://intl.cloud.tencent.com/document/product/248/38916).

### Creating trigger condition template[](id:Creating-trigger-condition-template)

1. Log in to the [CM console](https://console.cloud.tencent.com/monitor/).
2. On the left sidebar, click **Trigger Condition Template** to enter the **Template** list page.
3. Click **Create** on the **Trigger Condition Template** page.
4. On the **Create Template** page, configure the policy type.
   - **Policy Type**: select **TDMQ alarm** > **CMQ**.
   - **Use preset trigger condition**: select this option and the system recommended alarm policy will be displayed.
5. After confirming that everything is correct, click **Save**.
6. Return to the **Create Alarm Policy** page, click **Refresh**, and the alarm policy template just configured will be displayed.

