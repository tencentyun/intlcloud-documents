

## Backup Mode
TDSQL-C supports auto backup and manual backup.

## Backup Type
Different from traditional databases, TDSQL-C adopts the Redirect-On-Write (ROW) technology, which takes a snapshot of the disks at the storage layer for backup. The snapshot can be taken within one second, and the entire process is imperceptible to the businesses at the computing layer.

## Auto Data Backup
1. Log in to the [TDSQL-C console](https://console.cloud.tencent.com/cynosdb) and click a cluster name in the cluster list to enter the cluster management page.
2. On the cluster management page, select the **Backup Management** tab and click **Auto Backup Settings**.
![](https://main.qcloudimg.com/raw/409575a6cb8e798a0cff7df530a02893.png)
3. In the pop-up window, select the backup time period and click **OK**.
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody>
<tr>
<td>Backup Type</td><td>Currently, snapshot backup is supported.</td></tr>
<tr>
<td>Data Backup Retention</td><td>Data backup files can be retained for 7 days.</td></tr>
<tr>
<td>Start Time</td>
<td><ul><li>Backup start time. You can customize a time range as needed. We recommend you back up your database during off-hours.
<li>The default time range is 02:00 AM–06:00 AM. This is just the start time of the backup process and does not indicate the end time. <br>For example, if the time range is set to 02:00 AM–06:00 AM, the system will initiate a backup at a time point during 02:00 AM–06:00 AM, which depends on the backend backup policy and backup system conditions.</td></tr>
</tbody></table>

## Manual Data Backup
>?
>- Manual backup is supported only for full backup.
>- Manual backups can be manually deleted from the backup list in the console. You can delete manual backups that are no longer in use to free up space. Manual backups can be retained permanently as long as they are not deleted.
>
1. Log in to the [TDSQL-C console](https://console.cloud.tencent.com/cynosdb) and click a cluster name in the cluster list to enter the cluster management page.
2. On the cluster management page, select the **Backup Management** tab and click **Manual Backups**.
3. In the pop-up window, select the backup mode and objects and click **OK**.

