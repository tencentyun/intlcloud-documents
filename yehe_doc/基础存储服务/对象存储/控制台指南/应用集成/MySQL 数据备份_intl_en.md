## Overview

MySQL Backup is a [SCF](https://intl.cloud.tencent.com/document/product/583)-based feature provided by COS. It allows you to store data in TencentDB for MySQL to COS so that data can be stored persistently and protected from data loss or corruption. After you set a backup function rule for a bucket, SCF will scan your MySQL backup files periodically and store them in the bucket.

## Notes

- MySQL Backup functions only back up the backup files of TencentDB for MySQL. Therefore, if MySQL backup has not been enabled, the functions cannot be executed. For more information about TencentDB for MySQL backups, see [Backing up Databases](https://intl.cloud.tencent.com/document/product/236/37796).
- If you have added a MySQL backup rule to your bucket in the COS console, the backup function will appear in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default). **DO NOT** delete the function. Otherwise, your rule may not take effect.
- MySQL Backup is supported in SCF-enabled regions, including Guangzhou, Shanghai, Beijing, Chengdu, Hong Kong (China), Singapore, Mumbai, Toronto, and Silicon Valley. For more supported regions, see [SCF Documentation](https://intl.cloud.tencent.com/document/product/583).

## Directions

### Setting backup via Application Integration

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. On the left sidebar, click **Application Integration** > **Data Backup** and find **MySQL Backup**.
3. Click **Configure Backup Rule** to go to the rule configuration page.
4. Click **Add Function**.
>! If you haven't activated SCF, go to the [SCF console](https://console.cloud.tencent.com/scf) to activate it and authorize the service as instructed.
5. In the pop-up window, configure the following items:
 - **Function Name**: Uniquely identifies a function and cannot be modified after being set. You can view the function in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default).
 - **Associated Bucket**: A bucket to store the MySQL backup files
>!The MySQL data to be backed up must be in the same region as the associated bucket.
 - **Trigger Period**: Triggers the backup operation for the MySQL Backup function. Every day, every week, and custom periods are supported.
 - **Cron Expression**: If you use a custom period, you can use Cron to specify the trigger period rule. Cron follows the local Standard Time. For detailed configuration policies, see [Timer Trigger Description](https://intl.cloud.tencent.com/document/product/583/9708).
 - **Database Instance**: MySQL instance in the region where the current bucket resides
 - **Delivery Path**: Delivery path prefix of the backups. If not specified, backups will be stored in the root directory of the bucket.
 - **SCF Authorization**: SCF needs to be authorized so that it can read the MySQL instances as well as their backup files, and store the backup files to the specified bucket.
6. Click **Confirm**.
You can perform the following operations on the created function:
 - Click **Log** to view the historical running status of MySQL backup. If an error is reported, you can click **Log** to quickly redirect to the SCF console for viewing the error log details.
 - Click **More** > **Edit** to modify the MySQL data backup rule.
 - Click **More** > **Delete** to delete the unwanted MySQL backup rule.


### Setting backup via bucket configuration

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar and then click the desired bucket for the backup.
3. Click **Function Service** > **MySQL Backup Function**.
>! If you haven't activated SCF, go to the [SCF console](https://console.cloud.tencent.com/scf) to activate it and authorize the service as instructed.
4. Click **Add Function**.
5. In the pop-up window, configure the following items:
 - **Function Name**: Uniquely identifies a function and cannot be modified after being set. You can view the function in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default).
 - **Trigger Period**: Triggers the backup operation for the MySQL Backup function. Every day, every week, and custom periods are supported.
 - **Cron Expression**: If you use a custom period, you can use Cron to specify the trigger period rule. Cron follows China Standard Time (UTC+8:00). For detailed configuration policies, see [Cron Documentation](https://intl.cloud.tencent.com/document/product/583/9708).
 - **Database Instance**: MySQL instance in the region where the current bucket resides
 - **Delivery Path**: Delivery path prefix of the backups. If not specified, backups will be stored in the root directory of the bucket.
 - **SCF Authorization**: SCF needs to be authorized so that it can read the MySQL instances as well as their backup files, and store the backup files to the specified bucket.
6. Click **Confirm**.
You can perform the following operations on the created function:
 - Click **Log** to view the historical running status of MySQL backup. If an error is reported, you can click **Log** to quickly redirect to the SCF console for viewing the error log details.
 - Click **More** > **Edit** to modify the MySQL data backup rule.
 - Click **More** > **Delete** to delete the unwanted MySQL backup rule.
