TDSQL for MySQL has database audit capability, which can record accesses to databases and executions of SQL statements to help you manage risks and improve the database security.  
>?The database audit feature is currently in the beta testing. To use this feature, [submit a ticket](https://console.cloud.tencent.com/workorder/category).

## Enabling SQL Audit
1. Log in to the [TDSQL for MySQL console](https://console.cloud.tencent.com/tdsqld/instance-tdmysql), select **Database Audit** on the left sidebar, select a region at the top, click the **Audit Instance** tab, and click **Disabled** to filter audit-disabled instances.
![](https://qcloudimg.tencent-cloud.cn/raw/023dce8aca92a5f71f96edf4276810ef.png)
>?Alternatively, in **Audit Instance** on the **Audit Log** tab, directly search for audit-disabled instances and then enable audit for them.
>![](https://qcloudimg.tencent-cloud.cn/raw/0b388e192adf91a00891d4c64d5c5225.png)
2. On the **Audit Instance** tab, click the ID of the target instance to enter the enablement page, indicate your consent to the agreement, and click **Next**.
3. On the **Configure SQL Audit** page, select the audit log retention period and click **Enable**.
>?
>- You can select 7 days, 30 days, 3 months, 6 months, 1 year, 3 years, or 5 years as the audit log retention period. You can also modify it in the console after enabling audit. For more information, see [Modifying Log Retention Period](https://intl.cloud.tencent.com/document/product/1042/48429).
>- In order to meet the security compliance requirements for the retention period of SQL logs, we recommend you select 180 days or above.

## Viewing Audit Log
After enabling audit, you can view SQL audit logs on the **Audit Log** tab. For more information, see [Viewing Audit Logs] (https://intl.cloud.tencent.com/document/product/1042/48428)
