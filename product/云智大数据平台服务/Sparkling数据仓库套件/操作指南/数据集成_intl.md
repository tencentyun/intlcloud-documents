[//]: # (chinagitpath:XXXXX)

## Operation Scenario

Sparkling supports a variety of data ingestion methods:

- TencentDB data ingestion: Data in TencentDB can be ingested into Sparkling.
- COS data ingestion: You can create a bucket by generating an account key to ingest the data.

## Steps

### RDBMS Data Ingestion

1. Go to [Cluster Management](https://sparkling.cloud.tencent.com) and click **Data** in the left panel to enter the data ingestion page.
2. Configure the data source. ![](https://main.qcloudimg.com/raw/b9bb80180f6531b0c2ed73eb38cd1a4e.png)

   a. Select the **RDBMS** data type.
   b. Enter the **Server address** and **Port number** of TencentDB.
   c. Enter the **Username**, **Password**, **Database name** and **Table name** of the data table to be ingested.
> Click **Test connectivity** to verify whether it can be connected to the database where the data table to be ingested resides.
>
 d. Select the operation mode for the target table (**Create a table** or **Import an existing target table**) and enter the **Table name** and **Description**.
 e. Select the format type (**ORCFILE** or **PARQUET**).
3. After confirming that the information is correct, click **OK** to complete data ingestion.

### COS Data Ingestion

1. Click **Data** in the left panel to enter the data ingestion page.
2. Configure the data source. ![](https://main.qcloudimg.com/raw/eb1873256808e5797cd8ede21ab989b5.png)
   a. Data type: Select **COS** data type.
   b. Region: Select the region where the COS bucket is located.
   c. Authorization method: Select user key authorization.
   d. SecretID/SecretKey: Enter the generated key which can be viewed in the account information.
   e. Bucket: Enter the name of the bucket generated in COS and your appid. Click **View bucket** to view the data in the current bucket.
	 >? The bucket name needs to be entered in the <target bucket name-appid> format (e.g., sparkling-12334513). The bucket name and appid can be viewed in account information.
	 >
   f. Preview data: Click **Preview data** to preview the ingested data.
   g. Basic info: Enter the information of the ingested table.
   h. Storage info: Select the format type (**ORCFILE** or **PARQUET**).
3. After confirming that the information is correct, click **OK** to complete data ingestion.





