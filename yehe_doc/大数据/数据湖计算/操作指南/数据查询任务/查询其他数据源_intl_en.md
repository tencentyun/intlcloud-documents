Data Lake Compute allows you to query and analyze data in an external table. Currently, data from MySQL and EMR Hive can be connected to it. You can add and manage other data sources in the Data Lake Compute console.
## Adding a data source
1. Log in to the [Data Lake Compute console](https://console.cloud.tencent.com/dlc) and select the service region. You need to have the permission to create data catalogs.
2. Select **Data Explore** on the left sidebar, hover over **+**, and click **Create data catalog**.
![]()
3. Select the data source type. Currently, MySQL and EMR Hive are supported. Before configuring MySQL, you need to add the Data Lake Compute subnet to the database's allowlist. Two configuration methods are supported: database instance and JDBC connection.
![]()
	- Supported EMR Hive versions are 2.0.1, 2.1.0, 2.2.0, 2.2.1, 2.3.0, 2.4.0, 2.5.0, 2.5.1, and 2.6.0. The configuration is performed through the EMR access address.
4. Enter the data source information and click **Create connection**.
![]()

## Managing Data
Currently, Data Lake Compute allows you to **view the database information of** and **preview data in** external tables.

### Viewing database information
1. Log in to the [Data Lake Compute console](https://console.cloud.tencent.com/dlc) and select the service region. You need to have the permission to view data tables.
2. Select **Data Explore** on the left sidebar, hover over **+**, and click **Basic info**. You can view the basic information of a data table in the pop-up window.
![]()
![]()

### Previewing data in a data table
1. Log in to the [Data Lake Compute console](https://console.cloud.tencent.com/dlc) and select the service region. You need to have the permission to view data tables.
2. Select **Data Explore** > **Data table**, hover over **...**, and click **Preview data**. Then, you can run a SQL statement to query and display data in the data table.
![]()
