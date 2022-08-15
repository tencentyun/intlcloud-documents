Data Lake Compute provides a SQL editor for data query with standard SQL statements. The editor is compatible with SparkSQL.
You can enter the SQL editor from the **Data Explore** page and perform simple operations such as data management, multi-session data query, query record management, and download record management.

## Data Management
Data management supports adding data sources, managing databases, and managing data tables.
### Creating a data catalog
Currently, Data Lake Compute supports the management of COS and EMR Hive data catalogs. The directions are as follows:
1. Log in to the [Data Lake Compute console](https://console.cloud.tencent.com/dlc) and select the service region. You need to have the admin permission.
2. Select **Data Explore** on the left sidebar, hover over ![](https://qcloudimg.tencent-cloud.cn/raw/d963cf7b5aec5915e5369274e3b6939d.png) on the **Database & table** tab, and click **Create data catalog**.
![]()
For detailed directions, see [Querying Data from Other Sources](https://intl.cloud.tencent.com/document/product/1155/48673).

### Managing a database
You can create, delete, and view the details of a database in the SQL editor.

### Managing a data table
You can create, query, and view the details of a data table in the SQL editor.

### Changing the default database
You can use the SQL editor to specify the default database for query tasks. If no database is specified in a query statement, the query will be executed in the default database.
1. Log in to the [Data Lake Compute console](https://console.cloud.tencent.com/dlc) and select the service region.
2. Select **Data Explore** on the left sidebar, hover over the target database name, click ![](https://qcloudimg.tencent-cloud.cn/raw/ca9b8841e37d3f8b444146c0f9d5208f.png), and click **Set as default database** to set the database as the default database.
![]()
3. You can also change the default database in the **Default database** selection box.
![]()

## Data Query
### Managing a session
The SQL editor supports multiple sessions for data query. Each session is independently configured (with its own default database, compute engine, and query records), making it easier for you to run and manage multiple tasks.
- You can click ![](https://qcloudimg.tencent-cloud.cn/raw/c5576a8cc876cdde0ad4d5ea77e97c86.png) to create a session and click tabs to switch between editor pages.
![]()
- To facilitate the query and use, you can click **Save** to save a commonly used session and click ![](https://qcloudimg.tencent-cloud.cn/raw/3b2fd07bb785b3f1affa9e98cb36556f.png) to quickly open a saved session.
![]()
- For a saved session, you can click **Refresh** to update the saved information to ensure the accuracy of the query statement.
![]()
- The editor allows you to run multiple SQL statements concurrently. Click **Run** to run all the statements in the editor, which will be divided into multiple SQL tasks.
- To run some of the statements, select them and click **Partial run**.
![]()

### Viewing the query result
You can directly view query results in the SQL editor. You can also click ![](https://qcloudimg.tencent-cloud.cn/raw/1a1a6fab865faf251f9c2a88c72a3bf9.png) to show or hide query results.
![]()

- A single task can return up to 1,000 results in the console. 
- If no COS storage path is specified, you can download query results to your local system.

## Querying the run history
Each session saves the run history of three months and displays the query results in the last 24 hours. You can quickly find the information of a past task in **Run history**.
## Managing the download history
You can view the status and parameters of download tasks in each session in **Download history**.
![]()
