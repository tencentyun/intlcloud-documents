## Overview

This document describes how to configure a notification template in the alarm module in iPaaS.

You can quickly reuse a template for multiple policies to reduce repeated user notification configurations. You can customize the user notification methods; for example, you can configure alarm notification channels as Message Center, email, and SMS. You can also use different notification time periods for different users; for example, you can configure user A to receive alarm notifications in the daytime and user B to receive notifications at night.
You can create, edit, and delete notification templates.

## Prerequisites

- Viewing a notification template: The sub-account must have the project read permission in iPaaS.
- Creating/Editing/Deleting a notification template: The sub-account must have the project write permission in iPaaS.

> ?For more information on how to grant sub-accounts permissions, see [Granting Tencent Cloud Service Permissions](https://intl.cloud.tencent.com/document/product/248/36744).

## Use Limits

| Feature | Limit |
| -------- | --------------------------- |
| User notification | Up to five items can be added. |
| Webhook | Up to five URLs accessible over the public network can be entered. |

## Directions

[](id:new)
### Creating a notification template

1. Log in to the iPaaS console and select [**Alarm settings**](https://ipaas.tencentcloud.com/login) > **Notification templates**.
2. Click **Create** and enter basic information in **Create notification template**.
   - **Template name**: Enter a custom template name.
3. Configure the notification operation. The parameters are as detailed below:
	- **User notification**
> ?
> - [System admin](https://www.tencentcloud.com/document/product/1165/51574#.E8.85.BE.E8.AE.AF.E4.BA.91.E6.95.B0.E6.8D.AE.E8.BF.9E.E6.8E.A5.E5.99.A8.E8.A7.92.E8.89.B2) and [project admin](https://www.tencentcloud.com/document/product/1165/51574#.E8.85.BE.E8.AE.AF.E4.BA.91.E6.95.B0.E6.8D.AE.E8.BF.9E.E6.8E.A5.E5.99.A8.E8.A7.92.E8.89.B2): They can select all member accounts of the current project in the drop-down list.
> - [Project member](https://www.tencentcloud.com/document/product/1165/51574#.E8.85.BE.E8.AE.AF.E4.BA.91.E6.95.B0.E6.8D.AE.E8.BF.9E.E6.8E.A5.E5.99.A8.E8.A7.92.E8.89.B2): They can select only their own accounts.
> - [Ordinary member](https://www.tencentcloud.com/document/product/1165/51574#.E8.85.BE.E8.AE.AF.E4.BA.91.E6.95.B0.E6.8D.AE.E8.BF.9E.E6.8E.A5.E5.99.A8.E8.A7.92.E8.89.B2): They can select only their own accounts.
<table>
<thead>
<tr>
<th width="120px">Parameter</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Recipient</td>
<td>Select one or more users as recipients.</td>
</tr>
<tr>
<td>Time range</td>
<td>Define the time period for receiving alarms.</td>
</tr>
<tr>
<td>Recurrence</td>
<td>You can select days of the week for receiving notifications. By default, notifications are sent every day.</td>
</tr>
<tr>
<td>Notification type</td>
<td>Three alarm channels are supported: Message Center, email, and SMS. You can also set different channels and notification time periods for different users. For more information, see <a href="https://www.tencentcloud.com/document/product/1165/51643">Alarm Receiving Channel</a>.</td>
</tr>
</tbody></table>
	- **Webhook**
 <table>
<thead>
<tr>
<th width="120px">Parameter</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td><nobr>API URL</nobr></td>
<td>You can enter up to five URLs accessible over the public network as the callback API addresses, and iPaaS will push alarm messages to them promptly.
</tr>
<tr>
<td>Time range</td>
<td>Define the time period for receiving alarms.</td>
</tr>
</tbody></table>
> ? 
>- After the callback URL is saved successfully, when a created alarm policy is triggered or the alarm is cleared, the alarm messages will be pushed through webhook.
>- When a created alarm policy is triggered or the alarm is cleared, the alarm messages will be pushed through webhook. Webhooks also support repeated alarms.

>
4. Click **Confirm**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/15ec0b30d31d97a4b1184eb9b0539a99.png)


### Modifying a notification template

1. Log in to the iPaaS console and select [**Alarm settings**](https://ipaas.tencentcloud.com/login) > **Notification templates**.
2. Click the target template name to enter the editing page.
3. Edit the target content and click **Confirm**.


### Deleting a notification template

1. Log in to the iPaaS console and select [**Alarm settings**](https://ipaas.tencentcloud.com/login) > **Notification templates**.
2. Find the name of the target template, click **Delete** in the **Operation** column on the right, and confirm the deletion in the pop-up window.
> ?A template referenced by an alarm policy cannot be deleted. Cancel the reference in the alarm policy first before deleting the template.
>
![](https://qcloudimg.tencent-cloud.cn/raw/cd551e86184415fbf6fed1b2f2c8d099.png)
