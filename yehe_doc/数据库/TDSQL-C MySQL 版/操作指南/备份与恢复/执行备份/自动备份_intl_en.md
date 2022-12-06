TDSQL-C for MySQL supports automatic backup and manual backup. Automatic backup is enabled by default. You can configure backup policies for TDSQL-C for MySQL to automatically back up data as scheduled for guaranteed data security.

For a newly created cluster, TDSQL-C for MySQL automatically backs up data once a day (between 2:00 AM and 6:00 AM by default). You can customize the backup start time and retention period as needed in the console.

This document describes how to configure automatic backup in the console.

## Notes
- Automatic backup files cannot be deleted, but you can set the data and binlog backup retention period, so that they will be deleted upon expiration.
- You can view the **Backup Time** field in the data backup list to determine the exact time point of the data image in a backup file.

## Directions
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb).
2. Select the region at the top, find the target cluster in the cluster list, and click the cluster ID or **Manage** in the **Operation** column to enter the cluster management page.
3. On the cluster management page, select the **Backup Management** tab and click **Auto-Backup Settings**.
![](https://qcloudimg.tencent-cloud.cn/raw/002947d061fd7d247ae9981a2cb4565a.png)
4. In the pop-up window, configure the following items and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/9bad8b1e170763a97add30c250614b51.png)
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody>
<tr>
<td>Backup Type</td><td>Snapshot backup is selected by default.</td></tr>
<tr>
<td>Data Backup Retention</td><td>Data backup files can be retained for 7–1,830 days.</td></tr>
<tr>
<td>Start Time</td>
<td><ul><li>Backup start time. You can customize a time range as needed. We recommend you back up your database during off-peak hours.
<li>The default time range is 02:00–06:00 AM. This is just the start time of the backup process and does not indicate the end time. <br>For example, if the time range is set to 02:00–06:00 AM, the system will initiate a backup at a time point during 02:00–06:00 AM, which depends on the backend backup policy and backup system conditions.</td></tr>
<tr>
<td>Binlog Backup Retention</td><td>Binlog backup files can be retained for 7–1,830 days, which cannot be shorter than the data backup retention period.</td></tr>
</tbody></table>
5. The name of an automatic backup file is automatically generated. You can click the edit icon after the alias in the backup list to modify it.
![](https://qcloudimg.tencent-cloud.cn/raw/6bde18ff67e4f42f8b89e21088ae118e.png)
The settings window is as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/50b1cd287e6cd6b704345cc7b8cbfe50.png)
