Using the space analysis feature of DBbrain, you can view the instance space utilization, including the sizes of data and logs, the daily increase in space utilization, the estimated number of available days, and the space used by the tables and databases of the instance.

Currently, space analysis is supported only for TencentDB for MySQL (excluding the basic single-node instance).

## Disk Space
Log in to the [DBbrain console](https://console.cloud.tencent.com/dbbrain/slow-sql) and select **Performance Optimization** on the left sidebar. On the displayed page, select a database at the top and select the **Space Analysis** tab.

On the **Space Analysis** tab, you can view the daily average growth in the past week, the remaining disk space, the estimated available days, the daily distribution of disk usage, and the disk space trend in the past 30 days.
- For TencentDB for MySQL, the remaining disk space = purchased disk space - data space. 

![](https://main.qcloudimg.com/raw/ecd64ab4f412169e7a2fe6478ec18f04.png)

## Top Tables
>?You can manually refresh the top table/database data. Data is collected once a day by default. When the information is inaccurate due to the large difference between the data collection time and the current time, you can click **Refresh Manually** to collect and analyze the real-time data of top tables/databases. Note that there may be a slight delay when the instance has many databases and tables or when the access pressure is high.
>
The "Top Tables" section shows the details of the tables that have relatively high space usage. The table list in the section contains columns such as storage engine, physical file size, number of rows, total used space, data space, index space, fragmented space, fragmented rate, etc. Each column of data can be sorted in reverse order, and the real-time data can be refreshed manually.
You can view the disk space usage details in this section and perform optimization promptly.
![](https://main.qcloudimg.com/raw/714a962ec5ffc7489e3b9bd97c6286af.png)

The "Top Tables" section displays data by table. In the table list, you can click the row of a table to view its field and index information. The field information includes the table name, column name, field type, default value, whether the table is null, character set, sort, column position, and notes. The index information includes the table name, index name, whether the index is unique, included column, serial number, and cardinality.
![](https://main.qcloudimg.com/raw/74ed1a0565e84311907007565a0ec9dc.png)

In the table list, click the row of a table to view the space usage trend, including the trend of the physical file size, space usage (data space, index space, and total used space), and fragmented rate.
![](https://main.qcloudimg.com/raw/351385dd93a9683810619047e5545eba.png)


## Top Databases
The "Top Databases" section shows the details of the databases that have relatively high space usage. The database list in the section contains columns such as the physical file size, number of rows, total used space, data space, index space, fragmented space, fragmented rate, etc. Each column of data can be sorted in descending order.
You can view the disk space usage details in this section and perform optimization promptly. 
![](https://main.qcloudimg.com/raw/8dde50662da4c039668b0610a5324b81.png)

The "Top Databases" section displays data by database. In the database list, you can click the row of a database to view the space usage trend, including the trend of the physical file size, space usage (data space, index space, and total used space), and fragmented rate.
![](https://main.qcloudimg.com/raw/0577082b530d41c3c33c86fb59329cc2.png)
