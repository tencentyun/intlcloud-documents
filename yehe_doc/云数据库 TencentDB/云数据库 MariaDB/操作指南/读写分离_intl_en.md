
## Read/Write Separation Overview
#### Read/write separation
TencentDB for MariaDB supports read/write separation by default. Each replica in the primary/replica architecture can be read-only. If multiple replicas are configured, read requests will be automatically assigned to low-load replicas by the gateway cluster (TProxy).

#### Global automatic read/write separation
TencentDB for MariaDB supports global automatic read/write separation, i.e., all `SELECT` requests will be sent to replicas with no modification of the business required. To use this feature, you need to [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application and indicate "your account information, instance region, instance ID, request to enable automatic read/write separation, and consent to the global read/write separation risk statement".

**Risk of global read/write separation**
The replica naturally has data delay. In global automatic read/write separation, the system sends all `SELECT` requests to the replica by default with no policy provided (for more information, please see read/write separation based on read-only accounts). In this case, the business may read uncontrollable historical data, leading to data distortion. Therefore, this feature is only recommended for business systems that have no requirements of data consistency.
>!By submitting a ticket to enable this feature, you acknowledge that your business system can take this risk.


## Read/Write Separation Based on Read-only Accounts
A read-only account has only the read permission and reads data from the replica server (or read-only replicas) in a database cluster by default. In the [TencentDB for MariaDB console](https://console.cloud.tencent.com/mariadb), you can set a read-only account and a read policy on the **Account Management** tab of the instance management page.
![](https://main.qcloudimg.com/raw/15b490b02787a9f77fbbd512e8a1c3a6.png)
In read-only account settings, you can set **Read-only Request Allocation Policy** to define the read policy when a replica failure (or long delay) occurs. The **Read-only Replica Delay Parameter** defines the data sync delay time and is used together with **Read-only Request Allocation Policy**.
![](https://main.qcloudimg.com/raw/0c3479bf91b95b470037569fe95a8d13.png)
For example, if you design a transaction system, the following configuration items are recommended:
- Core transaction module: set a regular account which has read/write permission.
- Balance inquiry module: set a read-only account that reads from the replica by default, configure the request allocation policy so that the primary will be read from upon replica failure, and set the delay parameter to below 10 seconds in order to ensure primary/replica performance and data consistency of user inquiries.
- Batch inquiry module: set a read-only account that reads from the replica by default, configure the request allocation policy so that an error will be reported upon replica failure, and set the delay parameter to above 30 seconds in order to avoid affecting the primary performance.
In addition, the Multi-thread Asynchronous Replication (MAR) mechanism is to return a response immediately after data is written to a replica transaction log. In this case, replica table data may not be updated; therefore, delay will occur.

## Read/Write Separation Based on Comments


Add /*slave*/ field before each SQL to be executed by replica, and add `-c` parameter after `mysql` to resolve the annotation `mysql  -c -e  "/*slave*/sql"`, to automatically distribute the read request to replica. Examples are shown below:

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

## Read-only Replicas (Remote Read-only Replicas)
If the above read/write separation schemes do not meet your needs, TencentDB for MariaDB provides read-only replicas for you. A read-only replica is an independent database instance that does not participate in high-availability switch of the original primary instance and is used only for improving read performance.
