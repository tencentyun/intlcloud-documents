After setting an alarm policy, you need to add alarm recipients, which can be done during alarm notification configuration. This document describes how to set an alarm notification template in the console. When creating an alarm policy on the alarm policy configuration page, you can select an existing template or create a new one for easy configuration. You can also quickly apply the same template for multiple policies.

For more information on relevant limits and other descriptions, see [Creating Notification Template](https://intl.cloud.tencent.com/document/product/248/38922).

## Setting an alarm notification template
1. Log in to the [CM console](https://console.cloud.tencent.com/monitor/alarm2/notice) and select **Notification Template** on the left sidebar.
2. Click **Create**, configure the following items on the **Create Notification Template** page, and click **Complete**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/aX6u393_9.png)
<table>
<thead><tr><th width=10%>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Template Name</td>
<td>Enter the notification template name, which can contain up to 30 characters.</td></tr>
<tr>
<td>Notification Template</td>
<td>Select one or multiple notification templates. Options include **Alarm Trigger** and **Alarm Recovery**.</td></tr>
<tr>
<td>Notification Language</td>
<td>Select the notification language, which can be Chinese or English.</td></tr>
<tr>
<td>Recipient Object</td>
<td>Select users or user groups to receive notifications.</td></tr>
<tr>
<td>Notification Cycle</td>
<td>Select the notification cycle, which can be any number of days in a week.</td></tr>
<tr>
<td>Notification Period</td>
<td>Set the notification period. Alarm notifications will be sent at the start time in the notification cycle and will be stopped at the end time.</td></tr>
<tr>
<td>Receiving Channel</td>
<td>Select email, SMS, etc.</td></tr>
<tr>
<td>API URL</td>
<td>Enter a URL (domain name or IP[:port][/path]), webhook, DingTalk group chatbot webhook, or Slack group application webhook accessible over the public network, and CM will push alarm messages to the corresponding URL, DingTalk group, or Slack group (if the recipient is a user, there is no need to add an API callback).</td></tr>
</tbody></table>

 >!
 >- You need to enter the API callback only when pushing notifications to DingTalk group chatbots or Slack group applications.
 >- After the API callback is added, if the initial delivery of an alarm notification fails, CM attempts up to three retries with a delay between failed attempts set at 5 seconds.
 >- After the API callback is added, up to 20 notifications can be sent to each DingTalk group chatbot per minute. If this quota is exceeded, the traffic will be throttled for 10 minutes.


## Configuring an alarm notification
1. Log in to the [CM console](https://console.cloud.tencent.com/monitor/alarm2/policy) and select **Alarm Policy** on the left sidebar.
2 Click **Create** and select up to three alarm notification templates in **Configure Alarm Notification** in the **Configure Alarm Policy** window.
3. Click **OK** after configuring the alarm policy and notification.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/GKtj491_10.png)
4. After the configuration is completed, if an alarm is triggered by an exception, the system will send notifications to the recipients via the specified channels (email, SMS, and phone call).

