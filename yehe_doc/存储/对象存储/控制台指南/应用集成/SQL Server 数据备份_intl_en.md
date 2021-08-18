## Overview

SQL Server data backup is a [SCF](https://intl.cloud.tencent.com/document/product/583)-based database backup feature provided by COS. It allows you to dump SQL Server data to COS so that data can be stored persistently and stay safe from data loss or corruption. After you set a backup function rule for a specified bucket, SCF will scan your server backup files periodically and dump them in the bucket.

## Precautions

- SQL Server data backup functions back up only the backup files of SQL Server. If SQL Server backup is not enabled, the backup functions cannot be executed. For more information about SQL Server backup, please see [here](https://intl.cloud.tencent.com/document/product/238/35790).
- If you have added an SQL Server data backup rule to your bucket via the COS console, you can view it in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default). **DO NOT** delete the function. Otherwise, your rule may not take effect.
- Regions where SCF is available support SQL Server data backup, including Guangzhou, Shanghai, Beijing, Chengdu, Hong Kong (China), Singapore, Mumbai, Toronto, and Silicon Valley, and more. For more supported regions, please see [SCF Documentation](https://intl.cloud.tencent.com/document/product/583).

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. In the left sidebar, click **Application Integration** to go to the application integration management page.
3. In the **SQL Server Backup** area, click **Configure Backup Rule** to go to the rule configuration page.
4. Click **Add Function**.
>! If you haven't activated SCF, please go to the [SCF console](https://console.cloud.tencent.com/scf) to activate it and authorize the service as instructed.
>
5. In the pop-up window, configure the following information:
![](https://main.qcloudimg.com/raw/c0bfa86fbce604891e7dd0a4c7ba9a0d.png)
 - **Function Name**: uniquely identifies a function and cannot be modified after being set. You can view the function in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default).
 - **Associated Bucket**: bucket where SQL Server backup files are stored.
 - **Trigger Period**: triggers the backup operation for the SQL Server backup function. Every day, every week, and custom periods are supported.
 - **Cron Expression**: If you use a custom period, you can use Cron to specify the trigger period rule. Cron follows China Standard Time (UTC+8:00). For detailed configuration policies, please see [Cron Documentation](https://intl.cloud.tencent.com/document/product/583/9708).
 - **Database Instance**: SQL Server instance list of the region where the current bucket resides
 - **Delivery Path**: delivery path prefix of the backup files. If not specified, backup files will be stored in the root directory of the bucket.
 - **SCF Authorization**: SCF needs to be authorized so that it can read the SQL Server instances as well as their backup files, and save the backup files to the specified bucket.
6. Click **Confirm**.
![](https://main.qcloudimg.com/raw/864d9c513e8dd173b6c08cb8027a70e7.png)
You can perform the following operations on the created function:
 - Click **View Log** to view the historical running status of the SQL Server data backup. If an error is reported, you can click **View Log** to quickly redirect to the SCF console for viewing the error log details.
 - Click **Edit** to modify a SQL Server data backup rule.
 - Click **Delete** to delete an unwanted SQL Server data backup rule.
