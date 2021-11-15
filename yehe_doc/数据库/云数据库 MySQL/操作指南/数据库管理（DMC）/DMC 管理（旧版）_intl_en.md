This document describes the features of the legacy version of DMC, such as database/table creation, instance session management, real-time database monitoring, and InnoDB lock wait management.
>?
>- If you want to use features such as SQL window and visualized table data editing, you can click **Go to new version** on the navigation bar at the top to access the new version of DMC.
>- Currently, TencentDB for MySQL v8.0 does not support InnoDB lock wait management or phpMyAdmin.

## Database/Table Creation
1. Log in to [DMC](https://bj-dmc.cloud.tencent.com/v2/qcloudLogin/login) and select **Create** > **Create Database** > **Add Database** or **Create** > **Create Table** on the navigation bar at the top.
![](https://main.qcloudimg.com/raw/899520a477489601623a73558b9d5718.png)
2. In the pop-up dialog box, configure the new database/table and click **Submit**.
>?For more information on the character set and collation, please see [MySQL's official documentation](https://dev.mysql.com/doc/).
>
 - Database creation dialog box:
![](https://main.qcloudimg.com/raw/3d894dd9ca840274ce66321a84089d00.png)
 - Table creation dialog box:
![](https://main.qcloudimg.com/raw/4423064c24df9f0b083fec5281b428c7.png)

## Instance Session Management
Log in to [DMC](https://bj-dmc.cloud.tencent.com/v2/qcloudLogin/login), select **Instance Session** on the navigation bar at the top, and enter the instance session management page. You can view the details of all database sessions in the instance from four dimensions: session overview, users, access sources, and databases.
DMC allows you to kill sessions, facilitating your session management.
![](https://main.qcloudimg.com/raw/0c16ea83442b6c61f2d237f95b60e768.png)

## Real-Time Database Monitoring
Log in to [DMC](https://bj-dmc.cloud.tencent.com/v2/qcloudLogin/login), select **Instance Monitoring** on the navigation bar at the top, and enter the instance monitoring page. You can view the following monitoring data which is refreshed every four seconds:

|MySQL Status Information | InnoDB Row Operation | Threads | Network|
|---|---|---|---|
|`qps` indicates the number of queries responded per second | `read` indicates the number of read rows in the InnoDB storage engine table | `running` indicates the number of active connections, i.e., the number of connections where SQL statements are being executed | `in(KB)` indicates the inbound network traffic of the instance|
|`tps` indicates the number of transactions processed per second | `insert` indicates the number of written rows in the InnoDB storage engine table | `connected` indicates the number of idle connections to the instance, i.e., the number of connections where SQL statements have not been executed | `out(KB)` indicates the outbound network traffic of the instance|
|`ins` indicates the number of INSERT statements executed per second | `update` indicates the number of rows updated in the InnoDB storage engine table | - | - |
|`upd` indicates the number of UPDATE statements executed per second | `delete` indicates the number of rows deleted in the InnoDB storage engine table | - | - |
|`del` indicates the number of DELETE statements executed per second | - | - | - |
|`sel` indicates the number of SELECT statements executed per second | - | - | - |
|`hit` indicates the cache hit rate, which mainly refers to the hit rate of innodb_buffer_pool | - | - |- |



## Built-in phpMyAdmin
>?TencentDB for MySQL v8.0 does not support phpMyAdmin.
>
Log in to [DMC](https://bj-dmc.cloud.tencent.com/v2/qcloudLogin/login), select **Go to PMA** on the navigation bar at the top, and go to the built-in phpMyAdmin console to manage databases. The phpMyAdmin supports most MySQL features as follows:
- View and drop/delete databases, tables, views, fields, and indexes.
- Create, replicate, drop/delete, rename, and change databases, tables, fields, and indexes.
- Maintain servers, databases, tables, and relevant server configurations.
- Run and edit SQL statements.
- Manage stored procedures and triggers.

## DBbrain Intelligent Optimization
Log in to [DMC](https://bj-dmc.cloud.tencent.com/v2/qcloudLogin/login), select **DBbrain Intelligent Optimization** on the navigation bar at the top, and go to the DBbrain console.

