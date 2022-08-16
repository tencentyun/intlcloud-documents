Data Lake Compute allows you to quickly query and analyze COS data. Currently, CSV, ORC, Parquet, JSON, Avro, and text files are supported.
## Preparations
### Setting necessary internal permissions of Data Lake Compute
>? If you already have permissions or you are the root account admin, skip this step.

If you are logging in as a sub-account for the first time, in addition to the necessary CAM authorization, you also need Data Lake Compute permissions, which can be granted by a Data Lake Compute admin or root account admin through **Permission management** on the left sidebar in the Data Lake Compute console. For permission details, see [Permission Overview](https://intl.cloud.tencent.com/document/product/1155/48665).
1. Database and table permission: Permissions to read and write catalogs, databases, tables, and views can be granted.
2. Engine permission: Permissions to use, monitor, and modify compute engines can be granted.

>? By default, the system will activate the shared public engine based on the Presto kernel, so you can quickly try features out without purchasing a private cluster.

For detailed directions, see [Sub-Account Permission Management](https://intl.cloud.tencent.com/document/product/1155/48667).

## Analysis Steps
### Step 1. Create a database
If you are familiar with SQL statements, write the `CREATE DATABASE` statement in the query and skip the creation wizard.
1. Log in to the [Data Lake Compute console](https://console.cloud.tencent.com/dlc) and select the service region.
2. Select **Data Explore** on the left sidebar.
3. Select **Database & table**, click "+", and select **Create database** as shown below:
![]()
4. After selecting an execution engine in the top-right corner, run the `CREATE DATABASE` statement.
![]()


### Step 2. Create an external table
If you are familiar with SQL statements, write the `CREATE TABLE` statement in the query and skip the creation wizard.
1. Log in to the [Data Lake Compute console](https://console.cloud.tencent.com/dlc) and select the service region.
2. Select **Data Explore** on the left sidebar.
3. Select **Database & table**, select the created table, and right-click to select **Create external table wizard**.

>? An external table generally refers to a data file stored in a COS bucket under your account. It can be directly created in Data Lake Compute for analysis with no need to load additional data. It is external, so only its metadata will be deleted when you run `DROP TABLE`, while your original data will remain.

![]()

4. Generate the table creation statement based on the wizard, and then complete the steps of setting the basic information, selecting the data format, editing the column, and editing the partition.
	- Step 1. Select the COS path of the data file (which must be a directory in a COS bucket but not a bucket itself). There is also a quick method to upload a file to COS. The operations require relevant COS permissions.
![]()
	- Step 2. Select the data file format. In the **Advanced options**, you can select automatic inference, and then the backend will parse the file format and automatically generate the table column information for fast column inference.
![]()
>? Structure inference is an auxiliary tool for table creation and may not be 100% accurate. You need to check and modify the field names and types as needed.
>
![]()
	- Step 3. Skip this step if there is no partition. Proper partitioning helps improve the analysis performance. For more information on partitioning, see [Querying Partition Table](https://intl.cloud.tencent.com/document/product/1155/48671).
![]()
5. Click **Complete** to generate the SQL statement for table creation. Then, select a data engine and run the statement to create a table.
![]()


### Step 3. Run the SQL analysis
After the data is prepared, write the SQL analysis statement, select an appropriate compute engine, and start data analysis.
![]()

#### Sample
Write a SQL statement with all data query results being `SUCCESS` and run the statement after selecting a compute engine.
```
select * from `DataLakeCatalog`.`demo2`.`demo_audit_table` where _c5 = 'SUCCESS'

```
The execution result is as follows:
![]()






