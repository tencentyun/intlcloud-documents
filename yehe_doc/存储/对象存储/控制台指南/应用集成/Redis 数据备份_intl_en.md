## Overview

Redis Backup is a [SCF](https://intl.cloud.tencent.com/zh/document/product/583)-based database backup feature provided by COS. It allows you to save TencentDB for Redis data to COS so that data can be stored persistently and stay safe from data loss or corruption. After you set a backup function rule for a bucket, SCF will scan your Redis backups periodically and store them in the bucket.

## Notes

- Redis Backup functions back up only the backups of TencentDB for Redis. Therefore, if Redis Backup has not been enabled, the functions cannot be executed. For more information about TencentDB for Redis backup, please see [Backing Up TencentDB for Redis](https://intl.cloud.tencent.com/document/product/239/7071).
- If you have added a Redis Backup function rule to your bucket via the COS console, the function will appear in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default). **DO NOT** delete the function. Otherwise, your rule may not take effect.
- Regions where SCF is available support Redis Backup, including Guangzhou, Shanghai, Beijing, Chengdu, Hong Kong (China), Singapore, Mumbai, Toronto, and Silicon Valley, and more. For more supported regions, please see [SCF Documentation](https://intl.cloud.tencent.com/zh/document/product/583).

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. In the left sidebar, click **Application Integration** to go to the application integration management page.
3. In the **Redis Backup** area, click **Configure Backup Rule** to go to the rule configuration page.
4. Click **Add Function**.
>! If you haven't activated SCF, please go to the [SCF console](https://console.cloud.tencent.com/scf) to activate it and authorize the service as instructed.
>
5. In the pop-up window, configure the following information:
![](https://main.qcloudimg.com/raw/0cf850f5d3267b645f431520a19b0269.png)
 - **Function Name**: uniquely identifies a function and cannot be modified after being set. You can view the function in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default).
 - **Associated Bucket**: a bucket to store Redis backups
 - **Trigger Period**: triggers the backup operation for the Redis Backup function. Every day, every week, and custom periods are supported.
 - **Cron Expression**: If you use a custom period, you can use Cron to specify the trigger period rule. Cron follows China Standard Time (UTC+8:00). For detailed configuration policies, please see [Cron Documentation](https://intl.cloud.tencent.com/document/product/583/9708).
 - **Database Instance**: TencentDB for Redis instance in the same region where the current bucket resides
 - **Delivery Path**: delivery path prefix of the backups. If not specified, backups will be stored in the root directory of the bucket.
 - **SCF Authorization**: SCF needs to be authorized so that it can read the Redis instances as well as their backups, and store the backups to the specified bucket.
6. Click **Confirm**.
![](https://main.qcloudimg.com/raw/c2deab75a8e3ab68ab0c6f20d5f24f8e.png)
You can perform the following operations on the created function:
 - Click **View Log** to view the historical running status of Redis Backup. If an error is reported, you can click **View Log** to quickly redirect to the SCF console for viewing the error log details.
 - Click **Edit** to edit a Redis Backup rule.
 - Click **Delete** to delete an unwanted Redis Backup rule.
