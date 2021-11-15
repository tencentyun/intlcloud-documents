Tencent Cloud provides database audit capabilities for TencentDB for MySQL, which can record accesses to databases and executions of SQL statements to help you manage risks and improve the database security.  

>!Database Audit currently supports TencentDB for MySQL 5.6 and 5.7 (two-node and three-node) instances but not TencentDB for MySQL 5.5 or single-node instances.

## Audit Operations
### Creating audit rule
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/dls/mysql), select **Database Audit** on the left sidebar, select a region at the top, and click the **Audit Rule** tab.
2. On the **Audit Rule** tab, click **Create Rule**.
![](https://main.qcloudimg.com/raw/c4e92d4471a82b2c38d1bc78d8995044.png)
3. On the **Create Audit Rule** page, enter the rule name and description and click **Next**.
4. On the **Set Parameters** page, select the required audit mode and parameters and click **Save**.
>?After the rule is created successfully, it must be associated with an audit policy before it can take effect.
>
![](https://main.qcloudimg.com/raw/b6059e729814c6f585f9098370f5eef0.png)

### Enabling SQL audit
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/dls/mysql), select **Database Audit** on the left sidebar, select a region at the top, and click the **Audit Policy** tab.
2. On the **Audit Policy** tab, select the database instance for which to enable audit, indicate your consent to the agreement, and click **Next**.
![](https://main.qcloudimg.com/raw/f80b3ed667734c9aa1b00838a73fada0.png)
3. On the **Configure SQL Audit** page, select the audit log retention period and click **Next**.
>!In order to meet the security compliance requirements for the retention period of SQL logs, we recommend you select 180 days or above.
4. On the **Create a Policy** page, set the policy name, select the audit rule, and click **Create Policy**.

### Creating audit policy
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/dls/mysql), select **Database Audit** on the left sidebar, select a region at the top, and click the **Audit Policy** tab.
2. On the **Audit Policy** tab, click **Create Policy**.
![](https://main.qcloudimg.com/raw/9713931fcbd22e2f47d31b764c2d09c4.png)
3. In the pop-up window, set the policy name, select the audit rule, and click **OK**.

### Viewing audit log
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/dls/mysql), select **Database Audit** on the left sidebar, select a region at the top, and click the **Audit Log** tab.
2. In the **Audited Instance** section, select a database instance for which audit has been enabled to view its corresponding SQL audit logs. 
 - Click the time box and select a time period to view the related audit results in the selected time period.
 - In the text box, enter key tags or a key SQL command combination to search for and view related audit results.
>?
>- When entering multiple key tags in the text box for search, you can separate them by pressing Enter.
>- In the text box, you can enter key combination information such as SQL command, client IP, account, database, object name, policy name, execution time range, and number of affected rows.
>
![](https://main.qcloudimg.com/raw/33443b0991fb282782cf054d0cba0812.png)

## SQL Audit Fields
The following fields are supported in TencentDB for MySQL audit logs. You can click the following icon on the **Audit Log** tab in the [TencentDB for MySQL console](https://console.cloud.tencent.com/dls/mysql) to get and view the complete SQL audit logs.
![](https://main.qcloudimg.com/raw/b05298521cab82dd55c779f00fba150a.png)

| No. | Field Name | Description | Remarks |
| ---- | ------------- | ------------------------------------------------------------ | -------------------------------------- |
| 1    | host          | Client IP                                                     |   -                                           |
| 2    | dbname        | Database name                                                     |  -                                            |
| 3    | user          | Username                                                       |      -                                        |
| 4    | sql           | SQL statement                                                      |    -                                          |
| 5    | sqlType       | SQL statement type                                                  |   -                                           |
| 6    | errCode       | Error code                                                       | 0 indicates success                                    |
| 7    | affectRows    | Number of affected rows                                                     |     -                                         |
| 8    | checkRows     | Number of scanned rows                                                     |     -                                         |
| 9    | sentRows      | Number of returned rows                                                     |    -                                          |
| 10   | threadId      | Thread ID                                                       |       -                                       |
| 11   | ruleNum       | Audit rule ID                                                   |     -                                         |
| 12   | policyName    | Audit policy name                                                   |    -                                          |
| 13   | instanceName  | Instance name                                                       |    -                                          |
| 14   | timestamp     | Start time (s)                                               |   -                                           |
| 15   | nsTime        | Start Time (ns), which forms the start time accurate down to the nanosecond together with `timestamp` | Example: timestamp.nsTime 1577953020.887984015 |
| 16   | execTime      | Execution time (μs)                                            |    -                                          |
| 17   | cpuTime       | CPU time (ns)                                              |     -                                         |
| 18   | lockWaitTime  | Lock wait time (μs)                                           |    -                                          |
| 19   | ioWaitTime    | IO wait time (μs)                                           |     -                                         |
| 20   | trxLivingTime | Transaction execution time (μs)                                   |      -                                        |

## SQL Audit Rule
### Rule content
The following types are supported:
Client IP, database account, and database name. Supported operators are **include, not include, equal, and not equal**.

The full audit rule is a special rule, and all statements will be audited after it is enabled.

### Rule operation
- The different fields in each rule add the conditions; that is, the relationship between field and condition is "AND" (&&).
If the username is specified as "user1" with the operator being "equal", and the database name is specified as "test" with the operator being "equal", then only the actions of the "user1" user on the "test" database will be audited, and others will be ignored.
- The relationship between rules is "OR" (||).
You can specify one or more audit rules for an instance, and as long as any one of them is met, the instance should be audited. For example, if rule A specifies that only operations of user1 with an execution time >= 1 second need to be audited, and rule B audits the statements of user1 with an execution time < 1 second, then all statements of user1 need to be audited eventually.

### Rule description
Client IP, database account, and database name support **include, not include, equal, and not equal** operators, and only one operator can be set at a time, such as "not equal".
For "equal" and "not equal" operators, you can write multiple values and separate them by commas. For "include" and "not include" operators, you can write only one value. For example, if the operator is "equal", the value can be "user1,user2,user3".

#### Database name description
If a statement is of the following table object type:
```
SQLCOM_SELECT, SQLCOM_CREATE_TABLE, SQLCOM_CREATE_INDEX, SQLCOM_ALTER_TABLE,
SQLCOM_UPDATE, SQLCOM_INSERT, SQLCOM_INSERT_SELECT, SQLCOM_DELETE, SQLCOM_TRUNCATE, SQLCOM_DROP_TABLE
```
Then, for this type of operation, the name of the database actually manipulated by the statement shall prevail. For example, if the currently used database is "db3", and the statement is:
```
select *from db1.test,db2.test;
```
Then, "db1" and "db2" will be used as the target database for rule judgment. If the rule is configured to audit "db1", "db1" will be audited, and if the rule is configured to audit "db3", "db3" will not be audited.
For statements not of the above table object type, the currently used database will be used as the target database for rule judgment. For example, if the currently used database is "db1", and the executed statement is `show databases`, then "db1" will be used as the target database for judgment. If the rule is configured to audit "db1", "db1" will be audited.

### Notes
You can write only one value for "include" and "not include" operator. If you write multiple values, they will be treated as a string, resulting in incorrect matching.

