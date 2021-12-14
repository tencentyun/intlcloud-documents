# Configuring Basic Information
On an application’s details page, you can view and modify application information. On the **Basic Configuration** page, you can configure the message sending threshold, global SMS message sending limit, event callback, and sending frequency limit as needed, and manage alarm recipients.

## Message Sending Threshold Settings
1. Log in to the [SMS console](https://intl.cloud.tencent.com/login?s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fsmsv2).
2. You can enter the **Basic Configuration** tab in the following ways:
- Select **Application Management** > **Application List** on the left sidebar and click the block of the target application to enter its details page. Then, click **Basic Configuration**.
- Select **Application Management** > **Basic Configuration** on the left sidebar.
3. Select the **current application** as the target application to be manipulated.
4. Click **Set** in **Message Sending Threshold Settings** to set the message sending alarm threshold. Alarm recipients can receive the alarm notification when the threshold is reached. You can also set the message sending limit so that the application stops sending messages when the limit is reached that day.
![](https://qcloudimg.tencent-cloud.cn/raw/dde38d44364076d2ce64eeb48ed90fc2.png)
5. Click **Set** to save.
After that, please configure alarm recipients in **Notifications & Alarms** so that they can receive the notification when the threshold is reached.
![](https://qcloudimg.tencent-cloud.cn/raw/bab6b1bc059170bad7612e7fe998911c.png)

## Global SMS Message Sending Limit Settings
<dx-alert infotype="notice" title="">
This feature is supported only for organization users.
</dx-alert>
1. Click **Set** in **Global SMS Message Sending Limit Settings** to specify which countries/regions can receive SMS messages and set the message sending limit in a calendar day for each country/region.

![](https://qcloudimg.tencent-cloud.cn/raw/004b0e6423c3214962c0d7cdad7ee984.png)

2. You can either select a country/region one by one from the drop-down list or import multiple countries/regions by clicking **Batch Import**. Click **Download Template** to get the batch import template.
![](https://qcloudimg.tencent-cloud.cn/raw/fd0ebeef9e68b6bd55e0b84e56010a7e.png)

<dx-alert infotype="notice" title="">
- The message sending limit for a single country/region in a calendar day cannot exceed the total limit for all countries/regions.
- If left empty, it will be the same as the total limit by default.
- With these settings, the application can send messages only to the specified countries/regions.
</dx-alert>

3. Click **Set** to save.
If you want to modify the message sending limit for a single country/region in a calendar day later, click **Edit** in the **Operation** column. You can also delete or export the configured countries/regions.

## Event Callback Configuration
1. Click **Set** in **Event Callback Configuration**, select message status callback as needed, and enter the corresponding callback URL (callback information receipt API).
![](https://qcloudimg.tencent-cloud.cn/raw/8df55c41c5d708b2199e21849f4bb879.png)

<dx-alert infotype="explain" title="">
The body carried by the callback information is in JSON format.
</dx-alert>

2. Click **Set** to save.
After successful configuration, you will get a better grasp on the SMS delivery details. For example, after you configure the message receiving status callback address, Tencent Cloud will push the callback information received from the carrier to your specified callback address timely. Then, you can write appropriate code to receive, parse, and further use the callback information pushed by Tencent Cloud SMS.

![](https://qcloudimg.tencent-cloud.cn/raw/c2a11dac4c5cf3a3ab6ec18b42db488b.png)

## Setting a Sending Frequency Limit
To ensure business and channel security and minimize financial loss caused by malicious call of SMS APIs, the default frequency limit for sending SMS messages is set as follows:
- SMS messages with the same content can be sent to a single mobile number only once within 30 seconds.
- Up to 10 messages can be sent to the same mobile number in a calender day.

<dx-alert infotype="notice" title="">
>- Note: individual users have no permission to modify the frequency limit. To use this feature, change "Individual Verification" to "Organization Verification".
</dx-alert>

1. Click **Set** in **Sending Frequency Limit**, select the limits as needed, and set the corresponding threshold for each limit.
![](https://qcloudimg.tencent-cloud.cn/raw/6911eb24624726fc856d9b3af3457233.png)

2. Click **Set** to save.
![](https://qcloudimg.tencent-cloud.cn/raw/b6f36a9aa17e0aa82cbaa8ed81c21acb.png)

## Setting a Frequency Limit Allowlist

<dx-alert infotype="explain" title="">
> Mobile numbers in the allowlist are not subject to the frequency limit policy. An allowlist can contain up to 300 mobile numbers.
</dx-alert>

### Adding mobile number to allowlist
1. Click **Set** in **Frequency Limit Allowlist** and enter a mobile number per row. Up to 300 mobile numbers can be added to the allowlist.
![](https://qcloudimg.tencent-cloud.cn/raw/4d18af62c4e49d89db4de78e8d05cf20.png)

2. Click **Set** to save the settings.
![](https://qcloudimg.tencent-cloud.cn/raw/72c2f32c724fc4335db26b5e1592523a.png)

### Deleting mobile number from allowlist
1. Click **Delete** in the row of the target mobile number in **Frequency Limit Allowlist**.
![](https://qcloudimg.tencent-cloud.cn/raw/83ce9b62a99559d4d8a805e1acd5907c.png)
2. Click **Delete**.




