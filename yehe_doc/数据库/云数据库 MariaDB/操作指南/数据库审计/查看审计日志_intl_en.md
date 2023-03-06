## Viewing Logs
1. Log in to the [TencentDB for MariaDB console](https://console.cloud.tencent.com/mariadb), select **Database Audit** on the left sidebar, select a region at the top, and click the **Audit Log** tab.
2. In the audit instance section on the **Audit Log** tab, select a database instance with audit enabled to view its SQL audit logs. Or, on the **Audit Instance** tab, click an instance ID to enter the **Audit Log** tab and view audit logs.


### Tool list
![](https://qcloudimg.tencent-cloud.cn/raw/55ece67783162a16cdfeb5e857ad0d5f.png)
 - Click the time box and select a time period to view the audit results in the selected time period.
>?You can select any time period with data for search. Up to the first 60,000 eligible records can be displayed.
 - You can search by key tag to view audit results. Common key tags include SQL command, client IP, database name, database account, execution time, affected rows, and returned rows.
  - When entering multiple key tags in the text box for search, you can separate them by pressing **Enter**.
  - You can filter IP addresses by using the wildcard "*". For example, if you enter "client IP: 10.0.0.0*", IP addresses that start with "10.0.0.0" will be searched.

### Log list
- The **Returned Rows** field represents the specific number of rows returned by executing the SQL command, which is mainly used to determine the impact of `SELECT` commands.
- The **Affected Rows** field represents the specific number of rows modified by executing the SQL command, which is mainly used to determine the impact of rewrite commands.

## Audit Log Download
You can click the following icon on the **Audit Log** tab in the TencentDB for MariaDB console to obtain and view the complete SQL audit log.
![](https://qcloudimg.tencent-cloud.cn/raw/3a6059efd97654507d310a6e7583b947.png)

