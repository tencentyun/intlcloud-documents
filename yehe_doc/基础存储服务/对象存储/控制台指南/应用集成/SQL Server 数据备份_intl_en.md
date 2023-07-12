## Overview

SQL Server data backup is a [SCF](https://intl.cloud.tencent.com/document/product/583)-based database backup feature provided by COS. It allows you to dump SQL Server data to COS so that data can be stored persistently and protected from data loss or corruption. After you set a backup function rule for a specified bucket, SCF will scan your server backup files periodically and dump them in the bucket.

## Notes

- SQL Server data backup functions back up only the backup files of SQL Server. If SQL Server backup is not enabled, the backup functions cannot be executed. For more information about SQL Server backup, see [TencentDB for SQL Server](https://cloud.tencent.com/document/product/238/43296).
- If you have added a SQL Server data backup rule to your bucket in the COS console, you can view it in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default). **DO NOT** delete the function. Otherwise, your rule may not take effect.
- SQL Server data backup is supported in SCF-enabled regions, including Guangzhou, Shanghai, Beijing, Chengdu, Hong Kong (China), Singapore, Mumbai, Toronto, and Silicon Valley. For more supported regions, see [SCF Documentation](https://intl.cloud.tencent.com/document/product/583).

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. On the left sidebar, click **Application Integration** > **Data Backup**.
3. Find **SQL Server Backup** and click **Configure Backup Rule** to go to the rule configuration page.
4. Click **Add Function**.
>! If you haven't activated SCF, go to the [SCF console](https://console.cloud.tencent.com/scf) to activate it and authorize the service as instructed.
>
5. In the pop-up window, configure the following items:
<table>
   <tr>
      <th><b>Function Name</b></td>
      <td>Uniquely identifies a function and cannot be modified after being set. You can view the function in the <a href="https://console.cloud.tencent.com/scf/list?rid=1&ns=default">SCF console</a>.</td>
   <tr>
     <th><b>Associated Bucket</b></td>
      <td> A bucket to store SQL Server backup files.</td>
         </tr>
<th>Trigger Period</b></td>
      <td>Triggers the backup operation for the SQL Server backup function. Every day, every week, and custom periods are supported.</td>
   <tr>
      <th nowrap="nowrap"><b>Cron Expression</b></td>
      <td>If you use a custom period, you can use Cron to specify the trigger period rule. Cron follows the local Standard Time. For detailed configuration policies, see <a href="https://intl.cloud.tencent.com/document/product/583/9708">Timer Trigger Description.</a> </td>
   <tr>
   <th><b>Database Instance</b></td>
      <td>SQL Server instance list of the region where the current bucket resides</td>
   <tr>
      <th><b>Delivery Path</b></td>
      <td>Delivery path prefix of the backups. If not specified, backups will be stored in the root directory of the bucket.</td>
   <tr>
      <th><b>SCF Authorization</b></td>
      <td>SCF needs to be authorized so that it can read the SQL Server instances as well as their backup files, and save the backup files to the specified bucket.</td>
         </tr>
</table>

6. Click **Confirm**.
You can perform the following operations on the created function:
 - Click **Log** to view the historical running status of the SQL Server data backup. If an error is reported, you can click **Log** to quickly redirect to the SCF console for viewing the error log details.
 - Click **More** > **Edit** to modify the SQL Server data backup rule.
 - Click **More** > **Delete** to delete the unwanted SQL Server data backup rule.
