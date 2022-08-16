Storing data in partition catalogs can greatly reduce the scanned data volume of a computing task in Data Lake Compute and thereby significantly enhance the computing performance. The general practice of data partitioning is to store data in different catalogs by time. For example, data generated on the same day can be stored in the same catalog, and catalogs can be organized in a "year-month-day" structure. In Data Lake Compute, a table and its partitions must adopt the same data format.

## Creating a Partition Table
To create a partition table, you need to specify the partition field in the table creation statement.

## Adding Partitioned Data
Specifying a partition during data table creation is only to configure the partition field and doesn't allow running a query statement immediately to get data. You need to add partitioned data to a data table. If new partitioned data is added to the data catalog, you also need to add the partition information to the data table.

### Manually adding a partition
Use the `ALTER TABLE ADD PARTITION` statement to add a specified partition catalog to a data table. If the partition catalog is compatible with the Hive partitioning rule (**partition column name=partition column value**), you don't need to specify the data path; otherwise, you need to.
 - Sample 1: Adding a single partition catalog
```sql
ALTER TABLE tabel_demo ADD
PARTITION (dt = '2021-01-01');
```
 - Sample 2: Adding multi-level nested partition catalogs
```sql
ALTER TABLE tabel_demo ADD
PARTITION (year = '2021', month='01', day='01');
```
 - Sample 3: Displaying the specified partition path
```
ALTER TABLE tabel_demo ADD
PARTITION (year = '2021', month='01', day='01') LOCATION 'cosn://tablea_demo' ;
```

### Automatically adding a partition
Use the `MSCK REPAIR TABLE` statement to scan the data catalog specified during table creation. If there is a new partition catalog, the system will automatically add the partitions to the metadata of the data table. Below is a sample:
```sql
MSCK REPAIR TABLE table_demo
```

## System Restraints
- `MSCK REPAIR TABLE` only adds partitions to the metadata of the data table but does not delete them. To delete an added partition, run the `ALTER TABLE table-name DROP PARTITION` statement.
- `MSCK REPAIR TABLE` is not recommended if the data volume is large, as the system will scan all the data, which may take a long time, cause the task to time out, and make the partition information of the data table incomplete.
- A partition catalog must be compatible with the Hive partitioning rule of **partition column name=partition column value**; otherwise, use `ALTER TABLE ADD PARTITION` to load a partition.
- Make sure that data of a table is stored in a separate folder. For example, if the `cosn://tablea_a` data in table A and the `s3://table_a/table_b` data in table B are stored in COS and both tables are partitioned by string, then `MSCK REPAIR TABLE` will add partitions of table B to table A. To avoid this, use separate folder structures, such as `cosn://tablea_a`and `cosn://tablea_b`.
- The statement may incur data read/write fees charged by COS. For more information, see [Billing Overview](https://intl.cloud.tencent.com/document/product/436/16871).
