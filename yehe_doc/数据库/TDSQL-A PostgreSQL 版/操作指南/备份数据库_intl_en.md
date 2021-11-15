
To prevent data loss or corruption, you can use auto backup to back up your database.

## Auto Backup
1. Log in to the [TDSQL-A for PostgreSQL](https://console.cloud.tencent.com/tdsqla/tdapg) console and click an instance ID in the instance list to enter the instance management page.
2. On the instance management page, select **Backup** > **Auto Backup Settings** and click **Edit**.
![](https://main.qcloudimg.com/raw/6e1cb099245315a1732310240767fc6f.png)
3. On the editing page, enter the target value according to the prompt of **Backup Start Time** and click **OK**.
>?
>- Currently, only the backup start time can be modified.
>- Auto backups cannot be deleted manually. They will be deleted automatically upon expiration.
<table>
<thead><tr><th>Configuration Item</th><th>Value</th></tr></thead>
<tbody><tr>
<td>Data Backup Retention</td><td>7 days</td></tr>
<tr>
<td>Backup Time Interval</td><td>Once every 24 hours</td></tr>
<tr>
<td>Backup Start Time</td><td>00:00:00–02:00:00 AM</td></tr>
<tr>
<td>Enable Log Backup</td><td>No</td></tr>
</tbody></table>
<img src="https://main.qcloudimg.com/raw/e6edc6b244745b28789f12fc43ccd83d.png"  style="margin:0;">


