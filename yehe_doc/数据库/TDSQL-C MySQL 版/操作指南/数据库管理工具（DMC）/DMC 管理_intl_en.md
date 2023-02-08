This document describes the features of DMC, such as database/table creation, database management, instance session management, data import/export, and visualized table data editing.

## Database/Table creation
1. Log in to the DMC console.
 - Directly log in to the [DMC console](https://dms.cloud.tencent.com/#/login).
 - Or, log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb/mysql#/) and click **Log In** in the **Operation** column in the cluster list (list view).
 - Or, log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb/mysql#/), click the target cluster in the cluster list to enter the cluster management page, and click **Log In** in the top-right corner (tab view).
2. On the navigation bar, select **Create** > **Create Database** > **Create Database** or select **Create** > **Create Table**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/fUbf452_1.png)
3. In the pop-up window, configure the new database or table.
 - Database creation dialog box:
 ![](https://staticintl.cloudcachetci.com/yehe/backend-news/EiZ7742_2.png)
 - Table creation dialog box:
 ![](https://staticintl.cloudcachetci.com/yehe/backend-news/T8Vz645_3.png)

>?For more information on the character set and sorting rule, see [MySQL documentation](https://dev.mysql.com/doc/).

## Database management
Log in to the [DMC console](https://dms.cloud.tencent.com/#/login), select **Database Management** on the navigation bar at the top, and create, edit, or delete databases on the displayed page.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/iG9Q550_4.png)

## Instance session management
Log in to the [DMC console](https://dms.cloud.tencent.com/#/login), select **Instance Session** on the navigation bar at the top, and enter the instance session management page. You can view the details of all database sessions in the instance from four dimensions: session overview, users, access sources, and databases.
DMC allows you to kill sessions, facilitating your session management.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Tp6s308_5.png)

## SQL window
Log in to the [DMC console](https://dms.cloud.tencent.com/#/login), select **SQL Window** on the navigation bar at the top, or click **SQL Operation** on the **Operation** menu on the left sidebar to access the SQL window, which supports the following features:
- Run SQL commands and view results
- Optimize SQL statement formats
- View SQL command execution plans
- Save commonly used SQL statements
- Use SQL templates
- Export SQL statement execution results

![](https://staticintl.cloudcachetci.com/yehe/backend-news/Ctae415_6.png)

## Import/Export
Log in to the [DMC console](https://dms.cloud.tencent.com/#/login), select **Import/Export** > **Data Importing** or **Data Exporting** on the navigation bar at the top, and you can import data into or export data from a database.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/WjCa780_7.png)

## Visualized table data editing
DMC for TDSQL-C for MySQL supports inserting, deleting, and updating data. You can click a table in the table list on the left sidebar to insert, delete, and update its data in batches in the right pane, and then click **OK** in the **Quick Operation** pane to preview the SQL statements and implement the modification.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/EBgj885_8.png)

