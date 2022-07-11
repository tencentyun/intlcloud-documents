Tencent Cloud provides database audit capabilities for TencentDB for MySQL, which can record accesses to databases and executions of SQL statements to help you manage risks and improve the database security.  

>!Database Audit currently supports TencentDB for MySQL 5.6, 5.7, and 8.0 (two-node and three-node) instances but not TencentDB for MySQL 5.5 or single-node instances.

## [Creating Audit Rule](id:cjsjgz)
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/dls/mysql), select **Database Audit** on the left sidebar, select a region at the top, and click the **Audit Rule** tab.
2. On the **Audit Rule** tab, click **Create Rule**.
![](https://qcloudimg.tencent-cloud.cn/raw/687766a51c68c1b5ee483716c6097bac.png)
3. On the **Create Audit Rule** page, enter the rule name and description and click **Next**.
4. On the **Set Parameters** page, select the required audit mode and parameters and click **Save**.
>!
>- After the rule is created successfully, it must be associated with an audit policy before it can take effect.
>- For use instructions of SQL audit rules, see [SQL Audit Rule](https://intl.cloud.tencent.com/document/product/1102/47770).

## Enabling SQL Audit Service
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/dls/mysql), select **Database Audit** on the left sidebar, select a region at the top, click the **Audit Instance** tab, and click **Disabled** to filter instances whose audit is disabled.
![](https://qcloudimg.tencent-cloud.cn/raw/c64c25e2c28775636390079ba2971c91.png)
>?Alternatively, in **Audit Instance** on the **Audit Log** tab, directly search for instances whose audit is disabled and then enable audit.
>![](https://qcloudimg.tencent-cloud.cn/raw/8c8ed0771f0c0e81babe362e8d98c663.png)
2. On the **Audit Instance** tab, click the ID of the target instance to enter the enablement page, indicate your consent to the agreement, and click **Next**.
3. On the **Configure SQL Audit** page, select the audit log retention period and click **Next**.
>?
>- You can select 7 days, 30 days, 3 months, 6 months, 1 year, 3 years, or 5 years as the audit log retention period. You can also modify it in the console after enabling audit. For more information, see [Modifying Log Retention Period](https://intl.cloud.tencent.com/document/product/1102/47771).
>- In order to meet the security compliance requirements for the retention period of SQL logs, we recommend you select 180 days or above.
4. On the **Create a Policy** page, set the policy name, select a created [audit rule](https://intl.cloud.tencent.com/document/product/1102/47770), and click **Create a Policy**.

## Creating Audit Policy
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/dls/mysql), select **Database Audit** on the left sidebar, select a region at the top, and click the **Audit Policy** tab.
2. On the **Audit Policy** tab, click **Create Policy**.
![](https://qcloudimg.tencent-cloud.cn/raw/d5260ffd47d4318825a3ef152385dddd.png)
3. In the pop-up window, set the policy name, select a created [audit rule](https://intl.cloud.tencent.com/document/product/1102/47770), and click **OK**.

## Viewing Audit Log
After enabling audit, you can view SQL audit logs on the **Audit Log** tab. For more information, see [Viewing Audit Log](https://intl.cloud.tencent.com/document/product/1102/47772).

