Tencent Cloud provides database audit capabilities for TencentDB for MongoDB, which can record accesses to databases and executions of SQL statements to help you manage risks and improve the database security.

>!Database Audit currently supports TencentDB for MongoDB 4.0.

## Enabling SQL Audit Service
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/dls/mongodb), select **Database Audit** on the left sidebar, select a region at the top, click the **Audit Instance** tab, and click **Disabled** to filter instances whose audit is disabled.
![](https://qcloudimg.tencent-cloud.cn/raw/ea049e56295c6a20b47483dcb7134298.png)
>?Alternatively, in **Audit Instance** on the **Audit Log** tab, directly search for instances whose audit is disabled and then enable audit.
>![](https://qcloudimg.tencent-cloud.cn/raw/e53a8a137f788313d676d1385f25e4a1.png)
2. On the **Audit Instance** tab, click the ID of the target instance to enter the enablement page, select a log retention period, and click **Enable**.
>?
>- After audit is enabled for TencentDB for MongoDB, the rule is full audit.
>- You can select 7 days, 30 days, 3 months, 6 months, 1 year, 3 years, or 5 years as the audit log retention period. You can also modify it in the console after enabling audit. For more information, see [Modifying Log Retention Period](https://intl.cloud.tencent.com/document/product/1102/47771).
>- In order to meet the security compliance requirements for the retention period of SQL logs, we recommend you select 180 days or above.

## Viewing Audit Log
After enabling audit, you can view SQL audit logs on the **Audit Log** tab. For more information, see [Viewing Audit Log](https://intl.cloud.tencent.com/document/product/1102/47772).
