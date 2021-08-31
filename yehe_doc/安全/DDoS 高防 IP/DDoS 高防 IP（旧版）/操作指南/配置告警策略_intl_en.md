## Use Cases
You can create alarms when using an Anti-DDoS Advanced instance. The system will monitor relevant metrics based on alarm policies and trigger an alarm and send alarm messages to specified user groups when a metric meets the alarm condition. You can take appropriate precautionary or remedial measures in a timely manner based on the alarm message. Properly created alarms can help you improve the robustness and reliability of your applications. For more information on alarms, please see [Features](https://intl.cloud.tencent.com/document/product/248/38908) in Cloud Monitor.

## Alarm Trigger
If you want to monitor a metric of an instance, you need to create an alarm policy first, which is composed of three mandatory components: name, type, and alarm trigger. Each alarm policy is a set of alarm triggers. As long as one of the triggers is satisfied, the alarm will be triggered, and alarm messages will be sent to the specified users for them to check the alarm in time and take appropriate actions.
>You need to set the default alarm recipient; otherwise, the default alarm policy of Anti-DDoS Advanced will not be able to send notifications.

## Directions
### Creating alarm policies
1. Log in to the [Cloud Monitor Console](https://console.cloud.tencent.com/monitor/overview) and select **Alarm Configuration** > **Alarm Policy** on the left sidebar.
2. On the alarm policy list page, click **Add** to enter the policy creating page.
3. Set basic configuration items such as policy name and policy type. Select the service that needs alarming as the policy type. This document uses **Anti-DDoS Advanced** as an example.
4. Set the alarm object.
	- If you select **All Objects**, the alarm policy will be associated with all instances under the current account.
	- If you select **Certain Objects**, the alarm policy will be associated with the selected instances.
	- If you select **Instance Group**, the alarm policy will be associated with the selected instance group.
5. Set the alarm trigger. You can either choose a trigger template or configure a trigger on your own.
	- Trigger template
	Click **Trigger Template** to enable it and select a configured template from the drop-down list. For detailed configurations, please see [Configuring Trigger Templates](https://intl.cloud.tencent.com/document/product/248/38911). If a newly create template is not displayed, click **Refresh** on the right.
	- Trigger configuration
	An alarm trigger is a semantic condition consisting of metric, statistical period, comparison relationship, threshold, duration, and notification frequency.
	- Below is a sample parameter configuration:
		- Metric: connections.
		- Statistical Period: 1 minute.
		- Comparison Relationship: >.
		- Threshold: 100.
		- Duration: 2 statistical periods.
		- Notification frequency: once per day. This sample indicates that the number of connections will be collected once every minute, and an alarm will be triggered once per day if the number of connections of an Anti-DDoS Advanced instance is over 100 connections/minute for two consecutive times.
		>You can set the notification frequency to never repeat, every 5 minutes, every 10 minutes, exponential increase, or other frequencies. Exponential increase means that when an alarm is triggered for the first time, second time, fourth time, eighth time, ..., or 2 to the power of Nth time, alarm notifications will be sent. In other words, the alarm notification will be sent less and less frequently with longer time interval in between, reducing the disturbance caused by repeated notifications.
	
6. After confirming that everything is correct, click **Complete**.


### Associating with objects
After an alarm policy is created, you can associate some alarm objects with it. When an alarm object satisfies an alarm trigger, an alarm notification will be sent. You can associate an alarm object in the following steps:
1. Log in to the [Cloud Monitor Console](https://console.cloud.tencent.com/monitor/overview) and select **Alarm Configuration** > **Alarm Policy** on the left sidebar.
2. On the alarm policy management page, find the target policy and click its name to enter its details page.
3. In the alarm object section, click **Add Object**.
  >You can click **Add Object** under different regions. If you need to unassociate an alarm object, select the target instance and click **Unassociate** to unassociate it from the alarm policy.
3. On the configuration page, select the target Anti-DDoS Advanced instance and click **Apply** to associate it with the alarm policy.

### Setting alarm recipients
When a alarm is triggered, users in the alarm recipient group will receive the corresponding notification. You can set alarm recipients in the following steps:
1. Log in to the [Cloud Monitor Console](https://console.cloud.tencent.com/monitor/overview) and select **Alarm Configuration** > **Alarm Policy** on the left sidebar.
2. On the alarm policy management page, find the target policy and click its name to enter its details page.
3. In the alarm recipient section, click **Edit**.
4. On the configuration page, select the user group to be notified and receipt channel and click **Save**.
	- Currently, alarm notifications can be sent through email, SMS, WeChat, and phone. You can modify users' phone numbers, email addresses, or WeChat accounts in the [CAM Console](https://console.cloud.tencent.com/cam) as the receipt channel. For more information on how to modify user information, please see [Creating Sub-Users](https://intl.cloud.tencent.com/document/product/598/13674).
	-  For more information on how to enable the WeChat channel for alarm notifications in an alarm policy, please see Enabling WeChat Channel.
	-  If you want to enable the phone channel for alarm notifications in an alarm policy, please configure the following parameters.
		-  Number of Polls: it specifies the maximum number of calls made to all recipients in turn before they are reached.
		- Receipt Notification: a message will be sent to all recipients after the phone call is successfully made or the polling ends.
	 >
>- You can set the alarm recipients on the alarm policy creating page.
>- The phone channel for alarm notifications is currently in beta test. To try it out, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) or [contact us](https://intl.cloud.tencent.com/contact-sales) for application.
