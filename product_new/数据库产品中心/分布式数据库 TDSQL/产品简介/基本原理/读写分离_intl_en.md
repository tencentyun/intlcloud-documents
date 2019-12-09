## Overview
### Feature overview
When the read requests lead to high pressure and demand during processing of high volume of data, read-write separation can be used to distribute the read requests to slave nodes.
TDSQL supports read-write separation by default. Each slave in the master-slave architecture can be read-only. If multiple slaves are configured, read requests will be automatically allocated to low-load slaves by the gateway cluster (TProxy) to support the read traffic of large applications.

### How it works
Read-write separation is to separate read and write capabilities by letting the master node handle transactional operations (INSERT, UPDATE, and DELETE) and the slave nodes perform query operations (SELECT).

## Using Read-Write Separation
### Read-write separation based on read-only account
A read-only account is a type of account only with read permission to read data from a slave (or read-only instance) in a database cluster by default.
A read-only account can be used to implement automatic distribution of read requests to slaves and return results.
![](https://main.qcloudimg.com/raw/ae753538608bfd9139cfc875ef2e2a4f.png)
#### Read-write separation policy
In the settings of a read-only account, you can set the "read-only request allocation policy" to define the "read" policy when a slave fails (or lags for a long time).
 - Select **Master** to read from the master when the delay of the slave exceeds the limit.
 - Select **Report Errors** to report an error when the delay of the slave exceeds the limit.
 - Select **Read Only from Slave Server** to ignore the delay parameter and always read from the slave (this is generally used to pull binlog for sync).
 - Set the **Read-only slave server delay parameter** to define the data sync delay time, which is to be used together with **Master Server** and **Report Errors** under the **Read-only request allocation policy**.
![](https://main.qcloudimg.com/raw/f799fe198d5914b7a1f7231d4efa75e4.png)

### Read-write separation based on comment
Add a **```/*slave*/```** field before each SQL that needs to "read" from the slave, and add the `-c` parameter after `mysql` to parse the comment. For example, ```mysql -c -e "/*slave*/sql"``` can automatically allocate "read" requests to the slave. Below is the sample code:
```
//Read from master//
select * from emp order by sal, deptno desc;
//Read from slave//
/*slave*/ select * from emp order by sal, deptno desc;
```
>
>- Read from slave is supported only for the SELECT operation. Non-SELECT statements will fail.
>- The `-c` parameter needs to be added after `mysql` to parse the comment.
>- ```/*slave*/``` must be in lowercase, and no spaces are needed before and after the statement.
>- If the MAR mechanism (strong sync) is affected by slave exception, read from slave will be automatically switched to read from master.
