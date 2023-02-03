
## Read/Write Separation Overview
TencentDB for MariaDB supports read/write separation by default. Each replica in the primary/replica architecture can be read-only. If multiple replicas are configured, read requests will be automatically assigned to low-load replicas by the gateway cluster (TProxy).

## Read/Write Separation Based on Read-Only Accounts
A read-only account has only the read permission to read data from the replica server (or read-only instances) in a database cluster by default. In the [TencentDB for MariaDB console](https://console.cloud.tencent.com/mariadb), you can set a read-only account and a read policy on the **Account Management** tab of the instance management page.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/gB6M508_10.png)
In read-only account settings, you can set **Read-Only Request Allocation Policy** to define the read policy when a replica failure (or long delay) occurs. The **Read-Only Replica Server Delay Parameter** defines the data sync delay time and is used together with **Read-Only Request Allocation Policy**.
 -If **Primary Server** is selected, read from the primary server when the delay of replica server times out.
 If **Report Errors** is selected, report an error when all replica servers are delayed.

 - If **Read Only from Replica Server** is selected, ignore the replica delay and always read from replica server (generally used to fetch binlog for sync).
 - The **Read-Only Replica Server Delay Parameter** defines the data sync delay time.
<table>
<thead><tr><th>Allocation Policy</th><th>Read-Only Replica Server Is Specified</th><th>No Read-Only Replica Server Is Specified</th></tr></thead>
<tbody><tr>
<td>Primary Server</td>
<td>Read from the primary server when the actual delay exceeds the delay parameter.</td>
<td>Read from the other replica servers when the actual delay exceeds the delay parameter, and switch to the primary server when the delay of the replica server occurs.</td></tr>
<tr>
<td>Report Errors</td>
<td>An error will be reported when the actual delay exceeds the delay parameter.</td>
<td>Read from the other replica servers first when the actual delay exceeds the delay parameter, and an error will be reported when the delay of the replica server occurs.</td></tr>
<tr>
<td>Read Only from Replica Server</td>
<td>Read from the specified read-only replica </td>
<td>-</td></tr>
</tbody></table>
>?
>- To modify the settings of read-only account, select **More** > **Modify Read-Only Request Allocation Policy** in the **Operation** column.
>- If your instance architecture is 1-primary-1-replica, the read-only separation feature can only be used for low-load read-only tasks. Avoid high-load tasks such as large transactions, as they affect the backup tasks and availability of the replica server.


For example, if you design a transaction system, the following configuration items are recommended:
- Core transaction module: set a regular account which has read/write permission.
- Balance query module: Set a read-only account that reads from the replica by default, configure the request allocation policy so that the primary will be read from upon replica failure, and set the delay parameter to below 10 seconds in order to ensure primary/replica performance and data consistency of user inquiries.
- Batch query module: Set a read-only account that reads from the replica by default, configure the request allocation policy so that an error will be reported upon replica failure, and set the delay parameter to above 30 seconds in order to avoid affecting the primary performance.
In addition, the Multi-thread Asynchronous Replication (MAR) mechanism is to return a response immediately after data is written to a replica transaction log. In this case, replica table data may not be updated; therefore, delay will occur.

## Read/Write Separation Based on Comments

Add `/*slave*/` field before each SQL to be executed by replica, and add `-c` parameter after `mysql` to resolve the annotation `mysql  -c -e  "/*slave*/sql"`, to automatically distribute the read request to replica. Examples are shown below:
```
//Read data from primary//
select * from emp order by sal, deptno desc;
//Read data from replica//
/*slave*/ select * from emp order by sal, deptno desc;
```
>!
>- Only "read data from replica" (SELECT) is supported rather than other operations. Non-SELECT statements will fail.
>- `-c` parameter needs to be added after `mysql` to resolve the annotation.
>- `/*slave*/` must be lowercase, and no spaces are needed before and after the statement.
>- If the MAR mechanism is affected due to replica exception, the read operation on replica is automatically switched to that on primary.

## Read-only Instance (Remote Read-only Instance)
If the above read/write separation schemes do not meet your needs, TencentDB for MariaDB provides [read-only instance](https://intl.cloud.tencent.com/document/product/237/46722) for you. A read-only instance is an independent database instance that does not participate in high-availability switch of the original primary instance and is used only for improving read performance.
