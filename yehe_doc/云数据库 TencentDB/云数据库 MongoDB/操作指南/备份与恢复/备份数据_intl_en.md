
TencentDB for MongoDB by default automatically backs up on a daily basis, and you can also choose to back up data manually. This document describes how to back up data in the TencentDB for MongoDB console.
>?Backing up does not affect your business.

## Backup Type
- Physical backup: back up the physical database files of the instance. This type of backup is fast, has a high success rate, and is easy to restore.
- Logical backup: use mongodump to back up data. This type of backup is slow and requires connection to the instance.
>?
>- Physical backups cannot be used to roll back database tables.
>- Currently, physical backups are supported only in MongoDB v3.2.

## Automatic Backup
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb), click an instance ID in the instance list, and enter the instance management page.
2. Select **Backup and Rollback** > **Auto Backup Settings**, and click **Edit**.
3. Specify the following backup parameters and click **Save**.
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Data Backup Retention</td><td>By default, the data backups can be retained for seven days, which is currently free of charge.</td></tr>
<tr>
<td>Backup Interval</td><td>You can back up every 12 hours or every 24 hours (which is the default option).</td></tr>
<tr>
<td>Backup Start Time</td>
<td>Select one time period from the drop-down list. The default time period is 01:00-02:00, that is, the backup task will start at a point in time between 01:00 and 02:00 every day. The specific point in time varies with the schedule of the backup task.<br>When backups are performed every 12 hours (in which case, backups are performed twice in a day), the backup start time refers to the start time of the first backup.</td></tr>
<tr>
<td>Backup Exception Alert</td>
<td>Whether to notify users through Cloud Monitor events if an exception occurs while executing a backup task. Currently, only whitelisted users can use the Cloud Monitor events of TencentDB MongoDB. To get whitelisted, please <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a>. For more information about the supported TencentDB MongoDB events, please see<a href="https://intl.cloud.tencent.com/document/product/248/32823">Product Event List</a>.</td></tr>
</tbody></table>

## Manual Backup
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb), click an instance ID in the instance list, and enter the instance management page.
2. Click **Manual Backup** in the upper right corner.
3. In the pop-up dialog box, enter backup remarks and click **OK**.

