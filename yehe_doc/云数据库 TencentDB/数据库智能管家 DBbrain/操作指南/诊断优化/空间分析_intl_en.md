Using the space analysis feature of DBbrain, you can view the instance space utilization, including the sizes of data and logs, the daily increase in space utilization, the estimated number of available days, and the space used by tables and databases of the instance.

>?Currently, space analysis is supported only for TencentDB for MySQL (excluding the Basic Edition).

## Disk Space
Log in to the [DBbrain Console](https://console.cloud.tencent.com/dbbrain/slow-sql), select **Performance Optimization** on the left sidebar, and select **Space Analysis**.
On the "Space Analysis" tab, you can view the daily average growth in the past week, the remaining disk space (remaining disk space = purchased disk space - data space - log space), the estimated available days, the daily distribution of disk usage, and the disk space trend in the past week.
![](https://main.qcloudimg.com/raw/23ecbc61ef23db9fea532b75335712ad.png)

## Top Tables
>?You can manually refresh the top table/database data. Data is collected once a day by default. When the information is inaccurate due to the large difference between the data collection time and the current time, you can click **Refresh Manually** to collect and analyze the real-time data of top tables/databases. Note that there may be a slight delay when the instance has many databases and tables or the access pressure is high.
>
The "Top Tables" section shows the details of the tables that have relatively high space usage. The table list in the section contains such columns as storage engine, physical file size, number of rows, total used space, data space, index space, fragmented space, fragmented rate, etc. Each column of data can be sorted in descending order, and the real-time data can be refreshed manually.
You can view the disk space usage details in this section and perform optimization promptly.
![](https://main.qcloudimg.com/raw/68c0d625344d4fef8b10d9a5b57dbdba.png)

The "Top Tables" section displays data by table. In the table list, you can click the row of a table to view the field and index information. The field information includes table name, column name, field type, default value, whether to be nullable, character set, sort, column position, and remarks. The index information includes table name, index name, whether to be unique, included column, serial number, and cardinality.
![](https://main.qcloudimg.com/raw/e990f0bddad26516145d2d76bb73da40.png)

In the table list, click the row of a table to view the space usage trend, including the trend of physical file size, space usage (data space, index space, and total used space), and fragmented rate.
![](https://main.qcloudimg.com/raw/6a5d902cdf50bcabf962f13254cd5adb.png)


## Top Databases
The "Top Databases" section shows the details of the databases that have relatively high space usage. The database list in the section contains such columns as physical file size, number of rows, total used space, data space, index space, fragmented space, fragmented rate, etc. Each column of data can be sorted in descending order.
You can view the disk space usage details in this section and perform optimization promptly. 
![](https://main.qcloudimg.com/raw/45ba1e5ace7614a0fc2bc9dd1a6cbe8d.png)

The "Top Databases" section displays data by database. In the database list, you can click the row of a database to view the space usage trend, including the trend of physical file size, space usage (data space, index space, and total used space), and fragmented rate.
![](https://main.qcloudimg.com/raw/692aece908bc94c09a679ff64ef35650.png)
