### How long does it take to create a TencentDB for MySQL instance?
It generally takes less than 10 minutes to create a TencentDB instance. The time it takes to create read-only replicas is subject to the data volume of the source instance. The larger the data volume, the longer the time.
If it takes longer to create an instance, there may be something wrong. Please [contact us](https://intl.cloud.tencent.com/document/product/236/32996).

### How do I return a database?
You can log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb) and select **More** > **Terminate/Return** or **Terminate/Return & Refund** in the **Operation** column in the instance list to return an instance. For more information, please see [Terminating Instance](https://intl.cloud.tencent.com/document/product/236/31895).

<span id = "shilixiaohui"></span>
### What if a TencentDB for MySQL instance is terminated?
When an instance is returned, it will be retained in the recycle bin for a period of time. A pay-as-you-go instance will be retained for 1 day. During this period, you can go to the recycle bin and restore the instance.

<span id = "zhanghaomima"></span>
### What if I accidentally delete an account or forget the password?
- If you delete an account accidentally, you can log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), click an instance ID to enter the instance management page, and create an account by clicking **Database Management** > **Manage Account** > **Create** or by using an SQL statement. For more information, please see [Creating an Account](https://intl.cloud.tencent.com/document/product/236/31900).
- If you forget the root password, find the corresponding account in **Database Management** > **Manage Account** and click **More** > **Reset Password** in the **Operation** column. For more information, please see [Resetting Password](https://intl.cloud.tencent.com/document/product/236/31901).
The above operations can also be performed through the [ModifyAccountPassword](https://intl.cloud.tencent.com/document/product/236/17497) API.

### What is the maximum number of connections to TencentDB for MySQL? How do I modify it?
You can view the maximum number of connections to TencentDB for MySQL in the console. If the number of connections gets too high, you are recommended to locate the cause and solve the problem first instead of directly increasing the maximum value.
Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), click an instance ID to enter the instance management page, select **Database Management** > **Parameter Settings**, and modify the `max_connections` parameter.

### Why is the value of max_connections always displayed as 1,000 rather than the actual number of current maximum connections in MySQL instance monitoring?
`max_connections` represents the allowed maximum connections (1-100,000) in instance monitoring. Number of open connections means the number of connections available at the current moment, a value that changes in real time.

### How can I get to know that the disk capacity is insufficient?
The monitoring center oversees the disk capacity of a TencentDB instance. When the disk utilization is over 90%, SMS and email alarms will be triggered. You can configure alarm recipients in Cloud Monitor to receive such alarms. (For more information on how to configure, see [Alarm Policies (Cloud Monitor)](https://intl.cloud.tencent.com/document/product/236/8457)).

### How do I modify the case sensitivity of table name after a TencentDB for MySQL instance is initialized?
You need to adjust the `lower_case_table_names` parameter of the database.
Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), click the instance ID to enter the instance management page, select **Database Management** > **Parameter Settings**, and modify the `lower_case_table_names` parameter (`0`: case-sensitive, `1`: case-insensitive).
