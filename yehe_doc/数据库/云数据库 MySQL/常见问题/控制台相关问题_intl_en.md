### How long does it take to create a TencentDB for MySQL instance?
It generally takes less than 10 minutes to create a TencentDB instance. The time it takes to create read-only instances is subject to the data volume of the master instance. The larger the data volume, the longer the time.
If it takes longer to create an instance, there may be something wrong. Please [contact us](https://intl.cloud.tencent.com/document/product/236/32996) promptly.

### How do I return a database?
You can log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb) and select **More** > **Terminate/Return** or **Terminate/Return & Refund** in the "Operation" column in the instance list to return an instance. For more information, please see [Terminating Instance](https://intl.cloud.tencent.com/document/product/236/31895).

<span id = "shilixiaohui"></span>
### What if a TencentDB for MySQL instance is terminated?
When an instance is returned, it will be retained in the recycle bin for a period of time. A monthly subscription instance will be retained for 7 days and a pay-as-you-go instance for 1 day. During this period, you can go to the recycle bin and restore the instance.

<span id = "zhanghaomima"></span>
### What if I accidentally delete an account or forgot the password?
- If you delete an account accidentally, you can log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb), click an instance name to enter the instance management page, and create an account by clicking **Database Management** > **Manage Account** > **Create Account** or by using an SQL statement. For more information, please see [Creating Account](https://intl.cloud.tencent.com/document/product/236/31900).
- If you forgot the root password, find the corresponding account in **Database Management** > **Manage Account** and **reset password**. For more information, please see [Resetting Password](https://intl.cloud.tencent.com/document/product/236/31901).
The above operations can also be performed through [TencentCloud API](https://intl.cloud.tencent.com/document/product/236/17497).

### What is the maximum number of connections to TencentDB for MySQL? How do I modify it?
You can view the maximum number of connections to TencentDB for MySQL in the console. If the number of connections gets too high, you are recommended to locate the cause and solve the problem first instead of directly increasing the maximum value.
Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb), click an instance name to enter the instance management page, select **Database Management** > **Parameter Settings**, and modify the `max_connections` parameter.


### Why is the value of max_connections always displayed as 1,000 rather than the actual number of current maximum connections in MySQL instance monitoring?
max_connections represents the allowed maximum connections in instance monitoring. You can customize the maximum value up to 10,240. **Number of open connections** means the number of connections available at the current moment, a value that changes in real time.


### How can I get to know that the disk capacity is insufficient?
The monitoring center oversees the disk space of a TencentDB instance. When the disk utilization is over 90%, SMS and email alarms will be triggered. To receive such alarms, you only need to configure alarm recipients in Cloud Monitor. (For more information on how to configure, please see [Alarming Feature](https://intl.cloud.tencent.com/document/product/236/8457)).


### How do I modify the case sensitivity of table name after a TencentDB for MySQL instance is initialized?
You need to adjust the `lower_case_table_names` parameter of the database.
Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb), click the instance name to enter the instance management page, select **Database Management** > **Parameter Settings**, and modify the `lower_case_table_names` parameter (0: case-sensitive, 1: case-insensitive).
