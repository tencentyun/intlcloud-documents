## Overview

Redis Backup is a [SCF](https://www.tencentcloud.com/document/product/583)-based feature provided by COS. It allows you to store data in TencentDB for Redis to COS so that data can be stored persistently and protected from data loss or corruption. After you set a backup function rule for a bucket, SCF will scan your Redis backup files periodically and store them in the bucket.

## Notes

- Redis Backup functions back up only the backups of TencentDB for Redis. Therefore, if Redis Backup has not been enabled, the functions cannot be executed. For more information on TencentDB for Redis backup, see [Backing up Data](https://intl.cloud.tencent.com/document/product/239/7071).
- If you have added a Redis Backup function rule to your bucket via the COS console, the function will appear in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default). **DO NOT** delete the function. Otherwise, your rule may not take effect.
- Redis Backup is supported in SCF-enabled regions, including Guangzhou, Shanghai, Beijing, Chengdu, Hong Kong (China), Singapore, Mumbai, Toronto, and Silicon Valley. For more supported regions, see the [SCF documentation](https://www.tencentcloud.com/document/product/583).

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. On the left sidebar, click **Application Integration** > **Data Backup**.
3. Find **Redis Backup** and click **Configure Backup Rule** to go to the rule configuration page.
4. Click **Add Function**.
>! If you haven't activated SCF, go to the [SCF console](https://console.cloud.tencent.com/scf) to activate it and authorize the service as instructed.
>
5. In the pop-up window, configure the following items:

 - **Function Name**: Uniquely identifies a function and cannot be modified after being set. You can view the function in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default).
 - **Associated Bucket**: A bucket to store Redis backups
 - **Trigger Period**: Triggers the backup operation for the Redis Backup function. Every day, every week, and custom periods are supported.
 - **Cron Expression**: If you use a custom period, you can use Cron to specify the trigger period rule. Cron follows the Local Standard Time. For detailed configuration policies, see [Timer Trigger Description](https://intl.cloud.tencent.com/document/product/583/9708).
 - **Database Instance**: TencentDB for Redis instance in the same region where the current bucket resides
 - **Delivery Path**: Delivery path prefix of the backups. If not specified, backups will be stored in the root directory of the bucket.
 - **SCF Authorization**: SCF needs to be authorized so that it can read the Redis instances as well as their backups, and store the backups to the specified bucket.
6. Click **Confirm**.

You can perform the following operations on the created function:
 - Click **Log** to view the historical running status of Redis backup. If an error is reported, you can click **Log** to quickly redirect to the SCF console for viewing the error log details.
 - Click **More** > **Edit** to modify the Redis backup rule.
 - Click **More** > **Delete** to delete the unwanted Redis backup rule.
