## Read/write Separation Overview
#### Read/write separation
TencentDB for MariaDB supports read/write separation by default. Each slave in the master/slave architecture can be read-only. If multiple slaves are configured, read requests will be automatically assigned to low-load slaves by the gateway cluster (TProxy).

#### Global automatic read/write separation
TencentDB for MariaDB supports global automatic read/write separation, i.e., all `SELECT` requests will be sent to slaves with no modification of the business required. To use this feature, you need to [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application and indicate "your account information, instance region, instance ID, request to enable automatic read/write separation, and consent to the global read/write separation risk statement".

**Risk of global read/write separation**
The slave naturally has data delay. In global automatic read/write separation, the system sends all `SELECT` requests to the slave by default with no policy provided (for more information, please see read/write separation of read-only accounts). In this case, the business may read uncontrollable historical data, leading to data distortion. Therefore, this feature is only recommended for business systems that have no requirements of data consistency.
>By submitting a ticket to enable this feature, you acknowledge that your business system can take this risk.


## Read/Write Separation Based on Read-only Account
A read-only account only has read permission and reads data from the slave (or read-only instance) in a database cluster by default. In the TencentDB for MariaDB Console, you can set read-only account and read policy on the **Account Management** tab of the instance management page.
![](https://main.qcloudimg.com/raw/56a55745750f2fee5612119d7b5dd0f8.png)

In read-only account settings, you can set **Read-only Request Assignment Policy** to define the read policy when a slave failure (or long delay) occurs. The **Read-only Slave Delay Parameter** defines the data sync delay time and is used together with **Read-only Request Assignment Policy**.
![](https://main.qcloudimg.com/raw/1fc5dd033920c05e70ca73aec56ed810.png)

For example, if you design a transaction system, the following configuration items are recommended:
- Core transaction module: set a regular account which has read/write permission.
- Balance inquiry module: set a read-only account that reads from the slave by default, configure the request assignment policy so that the master will be read from upon slave failure, and set the delay parameter to below 10 seconds in order to ensure master/slave performance and data consistency of user inquiries.
- Batch inquiry module: set a read-only account that reads from the slave by default, configure the request assignment policy so that an error will be reported upon slave failure, and set the delay parameter to above 30 seconds in order to avoid affecting the master database performance.
In addition, the strong sync mechanism is to return a response immediately after data is written to a slave transaction log. In this case, slave table data may not be updated; therefore, delay will occur.

## Read/Write Separation Based on Comment
Add the ` /*slave*/ ` field before each SQL statement to be "read" by the slave, and add the `-c` parameter after "mysql" to parse the comment, such as `mysql  -c -e  "/*slave*/sql"`, to automatically assign read requests to the slave. Below are examples:

```
//Read from master//
select * from emp order by sal，deptno desc；
//Read from slave//
/*slave*/ select * from emp order by sal，deptno desc；
```

>
>- This feature only supports read from slave (SELECT) rather than other operations. Non-SELECT statements will fail.
>- The `-c` parameter needs to be added for the MySQL client to parse the comment.
>- `/*slave*/` must be in lowercase, and no spaces are needed before and after the statement.
>- If the MAR (strong sync) mechanism is affected by a slave exception, read from slave will be automatically switched to read from master.

## Read-only Instance (Remote Read-only Instance)
If the above read/write separation schemes do not meet your needs, TencentDB for MariaDB provides read-only instances for you. A read-only instance is an independent database instance that does not participate in high-availability switch of the original master instance and is used only for improving read performance. If needed, please contact your Tencent Cloud sales rep, architect, or after-sales services.
