## Overview

MySQL backup is a [Serverless Cloud Function](https://intl.cloud.tencent.com/document/product/583)-based feature provided by COS. It allows you to store data in TencentDB for MySQL to COS so that data can be stored persistently and stay safe from data loss or corruption. After you set a backup function rule for a bucket, SCF will scan your MySQL backup files periodically and store them in the bucket.

## Notes

- The MySQL backup function only backs up the backup files of TencentDB for MySQL. Therefore, if MySQL backup has not been enabled, the functions cannot be executed. For more information on TencentDB for MySQL backups, see [Backing up Databases](https://intl.cloud.tencent.com/document/product/236/37796).
- If you have added a MySQL backup rule to your bucket in the COS console, the backup function will appear in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default). **Do not** delete the function; otherwise, your rule may not take effect.
- Regions where SCF is available support MySQL backup, including Guangzhou, Shanghai, Beijing, Chengdu, Hong Kong (China), Singapore, Mumbai, Toronto, and Silicon Valley. For more supported regions, see [Serverless Cloud Function](https://intl.cloud.tencent.com/document/product/583).

## Directions

### Setting backup through application integration


1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. On the left sidebar, click **App Integration** and find **MySQL Data Backup**.
3. Click **Configure Backup Rule** to enter the rule configuration page.
4. Click **Add Function**.
>!
> If you haven't activated SCF, go to the [SCF console](https://console.cloud.tencent.com/scf) to activate it and authorize the service as instructed.
5. In the pop-up window, configure the following information:
![img](https://main.qcloudimg.com/raw/231eae263d09ea962c9901789505a61d.png)
 - **Function Name**: It uniquely identifies a function and cannot be modified after being set. You can view the function in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default).
 - **Associated Bucket**: It is the bucket to store the MySQL backup files.
 - **Trigger Period**: It triggers the backup operation for the MySQL backup function. Every day, every week, and custom periods are supported.
 - **Cron Expression**: If you use a custom period, you can use Cron to specify the trigger period rule. Cron follows China Standard Time (UTC+8:00). For detailed configuration policies, see [Timer Trigger Description](https://intl.cloud.tencent.com/document/product/583/9708).
 - **Database Instance**: It is the MySQL instance in the region where the current bucket resides.
 - **Delivery Path**: It is the delivery path prefix of the backups. If it is not specified, backups will be stored in the root directory of the bucket.
 - **SCF Authorization**: SCF needs to be authorized so that it can read the MySQL instances as well as their backup files and store the backup files in the specified bucket.
6. Click **Confirm**.
![img](https://main.qcloudimg.com/raw/1c7c9e1aaf5f99751ac0505e465815f3.png)
You can perform the following operations on the created function:
 - Click **View Log** to view the historical running status of MySQL data backup. If an error is reported, you can click **View Log** to quickly redirect to the SCF console to view the error log details.
 - Click **Edit** to modify a MySQL data backup rule.
 - Click **Delete** to delete an unwanted MySQL data backup rule.


### Setting backup through bucket configuration

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar and then click the target bucket to enter the **Bucket Management** page.
3. Click **Function Service** on the left and find **MySQL Backup Function**.
>! If you haven't activated SCF, go to the [SCF console](https://console.cloud.tencent.com/scf) to activate it and authorize the service as instructed.
>
4. Click **Add Function**.
5. In the pop-up window, configure the following information:
![](https://main.qcloudimg.com/raw/231eae263d09ea962c9901789505a61d.png)
 - **Function Name**: It uniquely identifies a function and cannot be modified after being set. You can view the function in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default).
 - **Trigger Period**: It triggers the backup operation for the MySQL backup function. Every day, every week, and custom periods are supported.
 - **Cron Expression**: If you use a custom period, you can use Cron to specify the trigger period rule. Cron follows China Standard Time (UTC+8:00). For detailed configuration policies, see [Timer Trigger Description](https://intl.cloud.tencent.com/document/product/583/9708).
 - **Database Instance**: It is the MySQL instance in the region where the current bucket resides.
 - **Delivery Path**: It is the delivery path prefix of the backups. If it is not specified, backups will be stored in the root directory of the bucket.
 - **SCF Authorization**: SCF needs to be authorized so that it can read the MySQL instances as well as their backup files and store the backup files in the specified bucket.
6. Click **Confirm**.
![img](https://main.qcloudimg.com/raw/1c7c9e1aaf5f99751ac0505e465815f3.png)
You can perform the following operations on the created function:
 - Click **View Log** to view the historical running status of MySQL data backup. If an error is reported, you can click **View Log** to quickly redirect to the SCF console to view the error log details.
 - Click **Edit** to modify a MySQL data backup rule.
 - Click **Delete** to delete an unwanted MySQL data backup rule.
