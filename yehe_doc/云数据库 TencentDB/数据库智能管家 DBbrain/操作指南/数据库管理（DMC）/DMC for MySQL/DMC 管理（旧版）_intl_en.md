This document describes the features of the legacy version of DMC, such as database/table creation, instance session management, real-time database monitoring, and InnoDB lock wait management.
>If you want to use features such as SQL window and visualized table data editing, you can click **Go to new version** on the navigation bar at the top to access the new version of DMC.

## Database/Table Creation
1. Log in to [DMC](https://bj-dmc.cloud.tencent.com/v2/qcloudLogin/login) and select **Create** > **Create Database** > **Add Database** or **Create** > **Create Table** on the navigation bar at the top.
![](https://main.qcloudimg.com/raw/d2784ca44212c731d5f78efda799556c.png)
2. In the pop-up dialog box, configure the new database/table and click **Submit**.
>For more information on the character set and sorting rules, please see [MySQL's official documentation](https://dev.mysql.com/doc/).
>
 - Database creation dialog box:
![](https://main.qcloudimg.com/raw/258605b4ac20f2136672bab0381e0f3f.png)
 - Table creation dialog box:
![](https://main.qcloudimg.com/raw/d2aec4106f019ff9d088be7c27737330.png)

## Instance Session Management
On the navigation bar at the top, click **Instance Session** to access the instance session management page. You can view the detailed session information of all instances in the current database and display the information by session overview, user, access source, and database.
DMC allows you to kill sessions, facilitating your session management.
![](https://main.qcloudimg.com/raw/dd87caaefb78386484ebb58bfdbdc6e4.png)

## Real-Time Database Monitoring
On the navigation bar at the top, click **Real-Time Monitoring** to access the real-time database monitoring page, which is refreshed once every four seconds and provides the following monitoring information:

MySQL Status Information | InnoDB Row Operation | Thread | Network
---|---|---|---
`qps` indicates the number of queries responded per second | `read` indicates the number of read rows in the InnoDB storage engine table | `running` indicates the number of active connections, i.e., the number of connections where SQL statements are being executed | `in(KB)` indicates the inbound network traffic of the instance
`tps` indicates the number of transactions processed per second | `insert` indicates the number of written rows in the InnoDB storage engine table | `connected` indicates the number of idle connections to the instance, i.e., the number of connections where SQL statements have not been executed | `out(KB)` indicates the outbound network traffic of the instance
`ins` indicates the number of INSERT statements executed per second | `update` indicates the number of rows updated in the InnoDB storage engine table | - | - |
[upd] indicates the number of UPDATE statements executed per second | `delete` indicates the number of rows deleted in the InnoDB storage engine table | - | - |
`del` indicates the number of DELETE statements executed per second | - | - | - |
`sel` indicates the number of SELECT statements executed per second | - | - | - |
`hit%` indicates the cache hit rate (mainly the hit rate of `innodb_buffer_pool`) | - | - |- |

## InnoDB Lock Wait Management
On the navigation bar at the top, click **InnoDB lock waits** to access the InnoDB lock wait management page. You can view the details of holdlocks and lock waits and delete sessions as shown below:
![](https://main.qcloudimg.com/raw/ea4ebed0ba1a6e8b804af1554c09d3e6.png)
![](https://main.qcloudimg.com/raw/746daa00522aa773c96c1248570a4537.png)

## Built-In phpMyAdmin
On the navigation bar at the top, click **Go to PMA** to access the built-in phpMyAdmin of DMC and perform relevant database operations. phpMyAdmin supports most MySQL features, including:
- View and drop/delete databases, tables, views, fields, and indexes.
- Create, replicate, drop/delete, rename, and change databases, tables, fields, and indexes.
- Maintain servers, databases, tables, and relevant server configurations.
- Run and edit SQL statements.
- Manage stored procedures and triggers.

## DBbrain Intelligent Optimization
On the navigation bar at the top, click **DBbrain Intelligent Optimization** to access the DBbrain Console.

