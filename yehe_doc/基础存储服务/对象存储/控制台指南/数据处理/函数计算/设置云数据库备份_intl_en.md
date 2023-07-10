## Overview

Cloud database backup is a [SCF](https://intl.cloud.tencent.com/document/product/583)-based database backup feature provided by COS. It allows you to store data in TencentDB to COS so that data can be stored persistently and stay safe from data loss or corruption. After you set a backup function rule for a specified bucket, SCF will scan your database backup files periodically and store them in the bucket.

## Notes:
- Cloud database backup functions back up only TencentDB backup files. Therefore, if database backup has not been enabled, the functions cannot be executed. For more information about TencentDB backups, please see [Backing up Databases](https://intl.cloud.tencent.com/document/product/236/37796).
- Currently, only backing up TencentDB for MySQL is supported.
- If you have added a cloud database backup function rule to your bucket via the COS console, the function will appear in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default). **DO NOT** delete the function. Otherwise, your rule may not take effect.
- Regions where SCF is available support cloud database backup, including Guangzhou, Shanghai, Beijing, Chengdu, Hong Kong (China), Singapore, Mumbai, Toronto, and Silicon Valley, and more. For more supported regions, please see [SCF Documentation](https://intl.cloud.tencent.com/document/product/583).

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** in the left sidebar and then click the desired bucket for the backup.
3. Click **Function Service** > **Cloud Database Backup Function**on the left.
> !If you haven’t activated SCF, please go to the [SCF console](https://console.cloud.tencent.com/scf) to activate it and authorize the service as instructed.
4. Click **Add Function**.
5. On the page that is displayed, configure the following items:
![](https://main.qcloudimg.com/raw/7559133c1df1478a1f6c44a1ba9f7820.png)
 - **Function Name**: uniquely identifies a function and cannot be modified after being set. You can view the function in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default).
 - **Trigger Period**: triggers the backup operation for the database backup function. Every day, every week, and custom periods are supported.
 - **Cron Expression**: If you use a custom period, you can use Cron to specify the trigger period rule. Cron follows China Standard Time (UTC+8:00). For detailed configuration policies, please see [Cron Documentation](https://intl.cloud.tencent.com/document/product/583/9708).
 - **Database Instance**: TencentDB instance list of the region where the bucket resides
 - **Delivery Path**: delivery path prefix of the backup files. If not specified, backup files will be stored in the root directory of the bucket.
 - **SCF Authorization**: SCF needs to be authorized so that it can read the TencentDB instances as well as their backup files, and store the backup files to the specified bucket.
6. Click **Confirm** to add the function.
![](https://main.qcloudimg.com/raw/477b6fd824f43aa4da9cfa5726b8de94.png)
You can perform the following operations on the created function:
 - Click **View Log** to view the historical running status of the database backup. If an error is reported, you can click **View Log** to quickly redirect to the SCF console for viewing the error log details.
 - Click **Edit** to modify the cloud database backup rule.
 - Click **Delete** to delete an unwanted cloud database backup rule.


