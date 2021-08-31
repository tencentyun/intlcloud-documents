This document describes the features of the new version of DMC, such as database/table creation, instance session management, SQL window, and visualized table data editing.
>If you want to use features such as real-time database monitoring and InnoDB lock wait management, you can click **Back to old version** in the top-right corner of the DMC navigation bar to access the legacy version of DMC.

## Database/Table Creation
1. Log in to [DMC](https://bj-dmc.cloud.tencent.com/v2/qcloudLogin/login) and select **Create** > **Create Database** > **Add Database** or **Create** > **Create Table** on the navigation bar at the top.
![](https://main.qcloudimg.com/raw/133ef0ed2eb8fee8c9262ea525782ee5.png)
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

## SQL Window
You can click **SQL Window** on the navigation bar at the top or click **SQL Operation** on the "Operation" menu on the left sidebar to access the SQL window page, which supports the following features:
- Run SQL commands and view results
- Optimize SQL statement formats
- View SQL command execution plans
- Save commonly used SQL statements
- Use SQL templates
- Export SQL statement execution results
![](https://main.qcloudimg.com/raw/feca011fc52d88d5ab989b2453a04c0e.png)

## Visualized Table Data Editing
The new version of DMC for MySQL supports data addition, deletion, and modification. You can click **Data Table** on the left sidebar to add, delete, and modify table data in batches. After completing data modification, you can click **OK** in the "Quick Operation" column to preview the modified SQL statements, and the modification will be implemented in batches after you confirm again.
![](https://main.qcloudimg.com/raw/d0d9b40bc3a6344c4259f6131bc3179a.png)
