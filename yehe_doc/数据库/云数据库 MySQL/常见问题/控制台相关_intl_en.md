### How long does it take to create a TencentDB for MySQL instance?
It generally takes less than 10 minutes to create a TencentDB instance. The time it takes to create read-only instances is subject to the data volume of the source instance. The larger the data volume, the longer the time.
If it takes longer to create an instance, there may be something wrong. [Contact us](https://intl.cloud.tencent.com/document/product/236/32996) for assistance.

### How do I return a database?
You can log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb) and select **More** > **Terminate/Return** or **Terminate/Return & Refund** in the **Operation** column in the instance list to return an instance. For more information, see [Terminating Instance](https://intl.cloud.tencent.com/document/product/236/31895).

[](id:shilixiaohui)
### What happens if a TencentDB for MySQL instance is terminated?
After an instance is returned, it will be retained in the recycle bin for seven days (in monthly subscription billing mode) or one day (in pay-as-you-go billing mode). During the retention period, it can be restored from the recycle bin.

[](id:zhanghaomima)
### What do I do if I accidentally delete an account or forget the password?
- If you delete an account accidentally, you can log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), click an instance ID to enter the instance management page, and create an account by clicking **Database Management** > **Account Management** > **Create Account** or by using a SQL statement. For more information, see [Creating Account](https://intl.cloud.tencent.com/document/product/236/31900).
- If you forgot the root password, find the corresponding account on the **Database Management** > **Account Management** tab and click **Reset Password**. For more information, see [Resetting Password](https://intl.cloud.tencent.com/document/product/236/31901).
The above operations can also be performed through the [ModifyAccountPassword](https://intl.cloud.tencent.com/document/product/236/17497) API.

### What is the maximum number of connections to TencentDB for MySQL? How do I modify it?
You can view the maximum number of connections to TencentDB for MySQL in the console. If the number of connections gets too high, we recommend you locate the cause and solve the problem first instead of directly increasing the maximum value.
Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), click an instance ID to enter the instance management page, select **Database Management** > **Parameter Settings**, and modify the `max_connections` parameter.

### Why is the value of max_connections always displayed as 1,000 rather than the actual number of current maximum connections in MySQL instance monitoring?
`max_connections` represents the allowed maximum number of connections (1–100,000) in instance monitoring. **Open Connections** indicates the number of connections available at the current moment, a value that changes in real time.

### How can I get to know that the disk capacity is insufficient?
The monitoring center oversees the disk capacity of a TencentDB instance. When the disk utilization is over 90%, SMS and email alarms will be triggered. You can configure alarm recipients in Cloud Monitor to receive such alarms. For more information on how to configure, see [Alarm Policies (Cloud Monitor)](https://intl.cloud.tencent.com/document/product/236/8457).

### How do I modify the case sensitivity of table name after a TencentDB for MySQL instance is initialized?
You need to adjust the `lower_case_table_names` parameter of the database.
Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), click the instance ID to enter the instance management page, select **Database Management** > **Parameter Settings**, and modify the `lower_case_table_names` parameter. Valid values are `0` (case-sensitive) and `1` (case-insensitive).
