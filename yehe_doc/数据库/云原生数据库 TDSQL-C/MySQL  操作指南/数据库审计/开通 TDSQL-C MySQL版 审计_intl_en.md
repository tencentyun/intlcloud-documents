
Tencent Cloud provides database audit capabilities for TDSQL-C for MySQL, which can record accesses to databases and executions of SQL statements to help you manage risks and improve the database security.  

## Enabling SQL Audit
1. Log in to the [TDSQL-C console](https://console.cloud.tencent.com/dls/cynosdb/instance), select **Database Audit** on the left sidebar, select a region at the top, click the **Audit Instance** tab, and click **Disabled** to filter instances whose audit is disabled.
![](https://qcloudimg.tencent-cloud.cn/raw/6292a68abb919dfed4daa0700cc2ef87.png)
>?Alternatively, in **Audit Instance** on the **Audit Log** tab, directly search for instances whose audit is disabled and then enable audit.
>![](https://qcloudimg.tencent-cloud.cn/raw/82b9a64177a32f2c6bc09f0f34803b5f.png)
2. On the **Audit Instance** tab, click the ID of the target instance to enter the enablement page, select a log retention period, and click **Enable**.
>?
>- You can select 7 days, 30 days, 6 months, 1 year, 3 years, and 5 years as the audit log retention period. You can also modify it in the console after enabling audit.
>- In order to meet the security compliance requirements for the retention period of SQL logs, we recommend you select 180 days or above.

## Viewing Audit Log
After enabling audit, you can view the corresponding SQL audit logs on the **Audit Log** tab.
