TDSQL-C for MySQL provides database audit capabilities to help you record accesses to databases and executions of SQL statements, so you can manage risks and improve the database security. This document describes how to enable the audit service in the console.

## Prerequisites
You have created a cluster as instructed in [Creating Cluster](https://www.tencentcloud.com/document/product/1098/52634).

## Directions
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb/mysql#/).
2. On the left sidebar, click **Database Audit**.
3. Click **Disabled** after **Audit Status** to filter instances for which the audit service is disabled.
4. Find the target instance in the audit instance list, or search for it by resource attribute in the search box, and click **Enable Database Audit** in the **Operation** column.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/6Mfa017_31.png)
>?You can batch enable the audit service for multiple target instances by selecting them in the audit instance list and clicking **Enable Database Audit** above the list.
>
![](https://staticintl.cloudcachetci.com/yehe/backend-news/XXvD744_32.png)
5. On the **Enable Database Audit** page, select the target audit instance, set the audit rule and the audit service, read and indicate your consent to the Tencent Cloud Terms of Service, and click **OK**.
 1. **Select the audit instance**
In the **Select Audit Instance** section, all instances selected in **step 4** are selected by default. You can select other or more target instances in this window or search for target instances by instance ID/name in the search box. Then, set the audit rule.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/5NNs172_33.png)
 2. **Set the audit rule**
In the **Audit Rule Settings** section, select **Full Audit** or **Rule-Based Audit**. Their differences are as detailed below:
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Full Audit</td>
<td>Full audit records all database accesses and SQL statement executions.</td></tr>
<tr>
<td>Rule-Based Audit</td>
<td>You can set audit rules for attributes of the TDSQL-C for MySQL database, such as <strong>client IP, username, database name, SQL details, and SQL type</strong>. Rule-based audit records the database accesses and SQL statement executions according to the custom audit rule.</td></tr>
</tbody></table>
<ul><li>If you select <b>Full Audit</b>, you can directly configure audit.</li>
<li>If you select <b>Rule-Based Audit</b>, you need to select **Create rule** or **Select from rule templates**. If you select an existing rule from rule templates, you can directly configure audit. If there are no appropriate rule templates, you can create a new one, refresh the page, and select it. For detailed directions, see <a href="https://www.tencentcloud.com/document/product/1098/53392">Creating Rule Template</a>.
</li>
<li>You can also select **Create rule** to directly create a rule as follows:
For the rule content, select the parameter field and operator and set the characteristic string for the parameter field as follows:
>?
>- You can configure one or multiple rules.
>- Different rules are in AND relationship; that is, they need to be met at the same time.
>- Different characteristic strings in a rule are in OR relationship; that is, at least one of them needs to be met.
>- You can add only one operator for the same parameter field; for example, for the database name, the operator can be either **Include** or **Exclude**.
</li></ul>
<table>
<thead><tr><th>Parameter Field</th><th>Operator</th><th>Characteristic String</th></tr>
</thead>
<tbody><tr>
<td>Client IP</td>
<td>Include, Exclude, Equal to, Not equal to</td>
<td>Up to five client IPs can be configured and should be separated by vertical bar "|".</td></tr>
<tr>
<td>Username</td>
<td>Include, Exclude, Equal to, Not equal to</td>
<td>Up to five usernames can be configured and should be separated by vertical bar "|".</td></tr>
<tr>
<td>Database Name</td>
<td>Include, Exclude, Equal to, Not equal to</td>
<td>Up to five database names can be configured and should be separated by vertical bar "|".</td></tr>
<tr>
<td>SQL Details</td>
<td>Include, Exclude, Equal to, Not equal to</td>
<td>Up to five SQL commands can be configured and should be separated by vertical bar "|".</td></tr>
<tr>
<td>SQL Type</td>
<td>Include, Exclude</td>
<td>Up to five SQL types can be selected. Valid options: ALTER, CHANGEUSER, CREATE, DELETE, DROP, EXECUTE, INSERT, LOGIN, LOGOUT, REPLACE, SELECT, SET, UPDATE, Other.</td></tr>
</tbody></table>

<b>Example</b>: If the following rule content is set: the database name should include `a`, `b`, or `c`, and the client IP should include IP1, 2 or 3, then the audit logs filtered by the rule are those where the database name includes `a`, `b`, or `c` and the client IP includes IP1, 2, or 3.

 3. **Configure audit**
In the **Configure audit** section, set the audit log retention period as well as frequent and infrequent access storage periods, read and indicate your content to the Tencent Cloud Terms of Service, and click **OK**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/AQLR881_34.png)
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Log Retention Period</td>
<td>Set the audit log retention period in days, which can be 7, 30, 90, 180, 365, 1,095, or 1,825.</td></tr>
<tr>
<td>Frequent Access Storage Period</td>
<td>Frequent access storage has the best query performance as it uses ultra high-performance storage media. Audit data is initially stored in frequent access storage for the time period specified here, after which it is automatically migrated to infrequent access storage. These two storage types only differ in performance but both support auditing. For example, if the log retention period is set to 30 days, and frequent access storage period is set to 7 days, then the infrequent access storage period will be 23 days by default.</td></tr>
</tbody></table>
