## Overview

CLS allows you to subscribe to a dashboard and export it as an image. Daily, weekly, and monthly reports can be emailed to specified recipients regularly.

## Usage Limits

Each account can have up to 100 subscription tasks.

## Directions

### Creating a subscription task

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls/overview).
2. On the left sidebar, click **View Dashboard** to enter the dashboard page.
3. Click **Subscription** at the top and select **Create Subscription Task** to enter the subscription configuration page.

4. Enter the **Task Name** and select the **Time Range** of the subscribed dashboard.

5. Set the **Variables** of the subscribed dashboard.

 - If you select **Default Configuration**, the default configuration items will be used for the variables of the subscribed dashboard. When the default variables change, the subscribed dashboard will also change.
 - If you select **Custom Configuration**, you can customize variables to render the subscribed dashboard.
6. Click **Preview Content** to preview the subscribed dashboard.
7. Select the subscription period, which can be by day, week, or month. Multiple weeks and months can be selected.

8. Configure the subscription method:
<table>
<thead>
<tr><th style="width: 20%">Type</th><th>Description</th></tr>
</thead>
<tbody><tr>
<td>Tencent Cloud user</td>
<td>Select a Tencent Cloud user as the email recipient of the subscribed dashboard. Users with no email address configured cannot receive email notifications.</td>
</tr>
<tr>
<td>Custom email address</td>
<td>Enter one or multiple custom email addresses.</td>
</tr>
</tbody></table>
9. Click **Send Immediately**, and CLS will send a subscription email to all the configured recipients.

### Managing a subscription task

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls/overview).
2. On the left sidebar, click **View Dashboard** to enter the dashboard page.
3. Click **Subscription** at the top and select **Manage Subscription Task** to enter the subscription task management page.

You can create, edit, or delete dashboard subscription tasks and view the last operation.
