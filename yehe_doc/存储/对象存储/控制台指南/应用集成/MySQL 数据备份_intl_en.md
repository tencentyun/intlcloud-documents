## Overview

MySQL Backup is a [SCF](https://intl.cloud.tencent.com/document/product/583)-based feature provided by COS. It allows you to store data in TencentDB for MySQL to COS so that data can be stored persistently and stay safe from data loss or corruption. After you set a backup function rule for a bucket, SCF will scan your MySQL backup files periodically and store them in the bucket.

## Notes

- MySQL Backup functions only back up the backup files of TencentDB for MySQL. Therefore, if MySQL backup has not been enabled, the functions cannot be executed. For more information about TencentDB for MySQL backups, please see [Backing up TencentDB for MySQL](https://intl.cloud.tencent.com/document/product/236/37796).
- If you have added a MySQL backup rule to your bucket via the COS console, the backup function will appear in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default). **DO NOT** delete the function. Otherwise, your rule may not take effect.
- Regions where SCF is available support MySQL Backup, including Guangzhou, Shanghai, Beijing, Chengdu, Hong Kong (China), Singapore, Mumbai, Toronto, and Silicon Valley, and more. For more supported regions, please see [SCF Documentation](https://intl.cloud.tencent.com/document/product/583).

## Directions

### Setting backup via Application Integration


1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Application Integration** in the left sidebar and then click **MySQL Backup**.
3. Click **Configure Backup Rule** to go to the rule configuration page.
4. Click **Add Function**.
>!
> If you haven’t activated SCF, please go to the [SCF console](https://console.cloud.tencent.com/scf) to activate it and authorize the service as instructed.
5. In the pop-up window, configure the following information:
![img](https://main.qcloudimg.com/raw/4b7aea0f5aacac472ba0dad0e491753f.png)
 - **Function Name**: uniquely identifies a function and cannot be modified after being set. You can view the function in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default).
 - **Associated Bucket**: a bucket to store the MySQL backup files
 - **Trigger Period**: triggers the backup operation for the MySQL Backup function. Every day, every week, and custom periods are supported.
 - **Cron Expression**: If you use a custom period, you can use Cron to specify the trigger period rule. Cron follows China Standard Time (UTC+8:00). For detailed configuration policies, please see [Cron Documentation](https://intl.cloud.tencent.com/document/product/583/9708).
 - **Database Instance**: MySQL instance in the region where the current bucket resides
 - **Delivery Path**: delivery path prefix of the backup files. If not specified, backup files will be stored in the root directory of the bucket.
 - **SCF Authorization**: SCF needs to be authorized so that it can read the MySQL instances as well as their backup files, and store the backup files to the specified bucket.
6. Click **Confirm** to add the function.
![img](https://main.qcloudimg.com/raw/450fcdb0b3ec29ad3e34c9df9f3526fe.png)
You can perform the following operations on the created function:
 - Click **View Log** to view the historical running status of MySQL Backup. If an error is reported, you can click **View Log** to quickly redirect to the SCF console for viewing the error log details.
 - Click **Edit** to modify a MySQL Backup rule.
 - Click **Delete** to delete an unwanted MySQL Backup rule.


### Setting backup via bucket configuration

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** in the left sidebar and then click the desired bucket for the backup.
3. Click **Function Service** > **MySQL Backup Function**.
>! If you haven't activated SCF, please go to the [SCF console](https://console.cloud.tencent.com/scf) to activate it and authorize the service as instructed.
>
4. Click **Add Function**.
5. In the pop-up window, configure the following information:
![](https://main.qcloudimg.com/raw/596f5789b2beacec2595adadf46ceaeb.png)
 - **Function Name**: uniquely identifies a function and cannot be modified after being set. You can view the function in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default).
 - **Trigger Period**: triggers the backup operation for the MySQL Backup function. Every day, every week, and custom periods are supported.
 - **Cron Expression**: If you use a custom period, you can use Cron to specify the trigger period rule. Cron follows China Standard Time (UTC+8:00). For detailed configuration policies, please see [Cron Documentation](https://intl.cloud.tencent.com/document/product/583/9708).
 - **Database Instance**: MySQL instance in the region where the current bucket resides
 - **Delivery Path**: delivery path prefix of the backup files. If not specified, backup files will be stored in the root directory of the bucket.
 - **SCF Authorization**: SCF needs to be authorized so that it can read the MySQL instances as well as their backup files, and store the backup files to the specified bucket.
6. Click **Confirm** to add the function.
![img](https://main.qcloudimg.com/raw/450fcdb0b3ec29ad3e34c9df9f3526fe.png)
You can perform the following operations on the created function:
 - Click **View Log** to view the historical running status of MySQL Backup. If an error is reported, you can click **View Log** to quickly redirect to the SCF console for viewing the error log details.
 - Click **Edit** to modify a MySQL Backup rule.
 - Click **Delete** to delete an unwanted MySQL Backup rule.
