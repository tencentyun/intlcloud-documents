## Operation Scenario
Sparkling supports a variety of data ingestion methods.

- TencentDB data ingestion: Data in TencentDB can be ingested into Sparkling.
- COS data ingestion: You can create a bucket by generating an account key to ingest the data.

In addition, Sparkling supports the incremental sync and scheduled data ingestion features of RDBMS, implementing incremental sync by importing data based on the timestamp and timed data ingestion by customizing the scheduling cycle.

## Directions

### RDBMS Data Ingestion
Go to [Cluster Management](https://intl.cloud.tencent.com/login) and click **Data** in the left navigation pane to enter the data ingestion page. Follow the steps below to complete the data ingestion from RDBMS:
![1](https://main.qcloudimg.com/raw/d6dc7bc2dc15778aab9a05996f377a8d.png)
##### 1. Configuring a Data Source
Select **RDBMS** for the data type, which supports **create a data source** and **import from an existing data source** for data ingestion.

Creating a data source:
   a. Select **Create a data source** for the ingestion method.
	 b. Select the region where the database is located. The stability and speed of cross-region database access may be geographically constrained.
	 c. Enter the TencentDB instance ID (which can be found in the [TencentDB console](https://intl.cloud.tencent.com/login)) and APPID (which can be found in [Account Information](https://intl.cloud.tencent.com/login) using the instance purchaser's account).
   d. Enter the **Username**, **Password**, **Database Name**, and **Table Name** of the data table to be ingested.
   e. Click **Test Connectivity** to verify whether it can be connected to the database where the data table to be ingested resides.
   f. After the system prompts that "Data connection is good", click **Next** to complete the data source configuration. You can also select **Save data source** to save the data source as an existing data source, so that when you ingest it next time, you can use the "Importing from an existing data source" method.
	 ![2](https://main.qcloudimg.com/raw/68148c054c2bbd10f31c0141ee14cd6f.png)

Importing from an existing data source
   a. Select "Importing from an existing data source" for the ingestion method.
	 b. Select an existing data source previously saved.
	 c. After entering the table name, click **Next** to complete the data source configuration.
	![3](https://main.qcloudimg.com/raw/7fdd064b9adf3f3cbfdd4e34bc1e3dbf.png) 

##### 2. Previewing Data
You can preview the field information in the data table on the "Data Preview" page. By default, five rows of data are extracted for preview. If there are no issues with the preview, click **Next**.
![4](https://main.qcloudimg.com/raw/747344ee460b436dd13b0f45cd7d7cfe.png)

##### 3. Configuring a Target
**Creating a table** or **Importing to an existing target table** are supported.

Creating a table:
a. Select **Create a table** and enter the **Title** and **Description**.
B. You can set the field name, description, and field order in the field definition and partition section. Field cropping is supported (i.e., you can delete unwanted fields and only import specified fields). The first column "pt" is the default partition field and cannot be deleted. By default, the timestamp is used as the partition value.
c. Select the format type (**ORCFILE** or **PARQUET**).
e. Check that there are no issues, then click **Next** to complete the target configuration by creating a table.
![5](https://main.qcloudimg.com/raw/e37d41f391162b302a0e9d42e865d806.png)

Import an existing target table:
a. Select **Import to an existing target table** and select the target table name.
b. Set the target partition. Select **Import to dynamic partition based on regular tasks** and the system will write the corresponding partition file based on your routine task configuration; if you select **Custom Partition**, please name the partition specifically according to the partition field.
c. Click **Field Mapping** to match the fields. If **Next** is grayed out, the field mapping failed. Please check whether the fields in the target table matches the fields to be imported in the source data table.
e. After ensuring that there are no issues, click **Next** to complete the target configuration by importing an existing target table.
![6](https://main.qcloudimg.com/raw/0f9f2dbf5ac0d8289c38df2d79d0792b.png)

##### 4. Configuring an Extraction Task
Two scheduling modes are supported: [once] and [regularly].

Once:
a. Select **Once** for the scheduling cycle.
b. The data loading mode can be **Timestamp-based incremental import** or **Full table import**. If **Timestamp-based incremental import** is selected, you need to add a filter condition. This method only imports data within the time range included in the filter condition; for details, see the syntax description. If **Full table import** is selected, you can select **Remove the existing data before writing new data (Insert Overwrite)** or **Keep the existing data (Insert)**.
e. After checking that there are no issues, click **Next** to complete the configuration of the one-time extraction task.
![7](https://main.qcloudimg.com/raw/0351f19134eb9827466af2cf1cdcae7b.png)

Regularly:
a. Select **Regularly** for the scheduling cycle.
b. Set the interval period, which can be daily, weekly, monthly, or hourly. For example, if you select 00:00 daily, the task will start running at 00:00 every day.
c. Set the regular task duration, i.e., the duration of the task, which can be one week, one month, three months, one year, or permanent.
d. The data loading mode can be **Timestamp-based incremental import** or **Full table import**. If **Timestamp-based incremental import** is selected, you need to add a filter condition. This method only imports data within the time range included in the filter condition; for details, see the syntax description. If **Full table import** is selected, you can select **Remove the existing data before writing new data (Insert Overwrite)** or **Keep the existing data (Insert)**.
e. After checking that there are no issues, click **Next** to complete the configuration of the routine extraction task.
![8](https://main.qcloudimg.com/raw/fe1f4bbd5b7f5dcb609a280f5e74b7bb.png)

##### 5. Previewing
You can view the current set data source, data preview, target table, and task scheduling on the "Preview" page. If there are no issues, click **Done** to complete the RDBMS data import task setup.

### COS Data Ingestion
1. Go to [Cluster management](https://intl.cloud.tencent.com/login) and click **Data** in the left pane to enter the data ingestion page.
2. Configure the data source. ![9](https://main.qcloudimg.com/raw/e82a5645c118608cae1cb423dc3ee0cc.png)
   - Data type: Select **COS** data type.
   - Region: Select the region where the COS bucket is located.
   - Authorization method: Select user key authorization.
   - SecretID/SecretKey: Enter the generated key which can be viewed in the account information.
   - Bucket: Enter the name of the bucket generated in COS and your APPID. Click **View Bucket** to view the data in the current bucket.
	 > The bucket name needs to be entered in a <target bucket name-APPID> format (e.g., sparkling-12334513). The bucket name and APPID can be viewed in the account information.
	 >
  - Preview data: Click **Preview Data** to preview the ingested data.
  - Basic information: Enter the information of the ingested table.
  - Storage information: Select the format type (**ORCFILE** or **PARQUET**).
3. Check that the information are all entered correctly, then click **Next** to perform data preview, target configuration, and preview operations. For more information, see RDBMS Data Ingestion.





