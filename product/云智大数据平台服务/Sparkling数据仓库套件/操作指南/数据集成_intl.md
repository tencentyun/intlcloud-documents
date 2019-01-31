[//]: # (chinagitpath:XXXXX)

## Operation Scenario

Sparkling supports a variety of data ingestion methods:

- TencentDB data ingestion: Data in TencentDB can be ingested into Sparkling.
- COS data ingestion: You can connect a bucket by generating an account key to ingest the data.

In addition, Sparkling supports the incremental sync and timed data ingestion features of RDBMS, implementing incremental sync by importing data based on the timestamp and timed data ingestion by customizing the scheduling interval.
## Steps

### RDBMS Data Ingestion

1. Go to [Cluster management](https://sparkling.cloud.tencent.com) and click **Data** in the left pane to enter the data ingestion page.
2. Configure the data source. ![](https://main.qcloudimg.com/raw/eb92b8de6e610aa7fb3a77b746ee09c9.png)
   a. Select the **RDBMS** data type.
   b. Enter the **Server address** and **Port number** of TencentDB.
   c. Enter the **Username**, **Password**, **Database name** and **Table name** of the data table to be ingested.
> Click **Test connectivity** to verify whether it can be connected to the database where the data table to be ingested resides.
>
 d. Click **Preview table** to view the table preview information.

3. Select the operation mode for the target table (**Create a table** or **Import to an existing target table**).
**Create a table**
![](https://main.qcloudimg.com/raw/ec26c1d2cd25f7a9a44841dbb3ce4f7b.png)
a. Select **Create a table** and enter the **Title** and **Description**.
b. In the storage information section, you can set the field name, description, partition value and field order. Field clipping is supported (i.e., importing certain fields by deleting other ones). You can click the <img src="https://main.qcloudimg.com/raw/4b6a2b1323506799dbdfb1db1a38b978.png"  style="margin:0;"> button to set the field as the partition column.
c. Select the format type (**ORCFILE** or **PARQUET**).
d. Set the timed task configuration. In creating table mode, only one-time scheduling is supported. The loading mode can be **Timestamp-based incremental import** or **Full table import**. If **Timestamp-based incremental import** is selected, you need to add a filter condition. This method only imports data within the time range included in the filter condition; for details, see the syntax description. If **Full table import** is selected, you can select **Remove the existing data before writing new data (Insert Overwrite)** or **Keep the existing data (Insert)**.
e. After confirming that the information is correct, click **OK** to complete the data ingestion in creating table mode.

 **Import to an existing target table**
![](https://main.qcloudimg.com/raw/1048474093b2a8b80c63f2fb322a8c09.png)
a. Select **Import to an existing target table** and then select the **Target table name** and **Target partition** as prompted. Click **Field mapping** to match the fields to those in the database with the same field name and type.
b. Set the timed task configuration. You can select to schedule **Once** or **Regularly** scheduling. For more information about **one-time** scheduling, see the timed task configuration method in the creating table mode above. If **Regular** scheduling is selected, you need to set the interval and time, for example, 00:00 daily indicates that the task starts automatically at 00:00 every day. You can complete the timed task configuration by selecting the appropriate regular task duration, concurrent/serial settings, data loading mode and overwrite rule.
>  After the scheduling period is set, the first execution of the task will be at the start time + one scheduling period.
>
![](https://main.qcloudimg.com/raw/ca9e8753e5f1a596388f6a02f645fc3a.png)
c. After confirming that the information is correct, click **OK** to complete the data ingestion in importing to existing target table mode. The details of the datasync task can be viewed in the **Tasks** column on the left.

### COS Data Ingestion
1. Click **Data** in the left pane to enter the data ingestion page.
2. Configure the data source. ![](https://main.qcloudimg.com/raw/28f5ca96f19728b78cc0a47204307b51.png)
   a. Data type: Select the **COS** data type.
   b. Region: Select the region where the COS bucket is located.
   c. Authorization method: Select user key authorization.
   d. SecretID/SecretKey: Enter the generated key which can be viewed in the account information.
   e. Bucket: Enter the name of the bucket generated in COS and your appid. Click **View bucket** to view the data in the current bucket.
    > The bucket name needs to be entered in the "target bucket name-appid" format, e.g., sparkling-12334513. The bucket name and appid can be viewed in the account information.
     >
   f. Preview data: Click **Preview data** to preview the ingested data.
   g. Basic information: Enter the information of the ingested table.
   h. Storage information: Select the format type (**ORCFILE** or **PARQUET**).
3. After confirming that the information is correct, click **OK** to complete data ingestion.



