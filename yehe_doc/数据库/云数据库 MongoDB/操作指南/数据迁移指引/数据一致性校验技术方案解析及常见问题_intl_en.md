During data consistency check, DTS compares the collection data between the source and target databases and outputs the comparison result and inconsistency details for you to perform a business cutover stably and reliably. 

## Check Scheme
DTS checks and compares all the data migrated during full migration and incremental migration from the source database. A full data check compares the data in the source and target databases row by row. Once the thread of the incremental data check finds that the full data comparison is completed, it immediately starts the incremental data check to get the start timestamp of the full data check, get the incremental oplog in the source database in a loop, and compare the differences between the source and target databases. When the time lag of data in the source and target databases is below 10 seconds, the comparison ends, and the check result is output.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/KC4t589_PRELIM__%E4%BA%91%E6%95%B0%E6%8D%AE%E5%BA%93%20MongoDB_%E4%BA%A7%E5%93%81%E7%9B%AE%E5%BD%95_%E4%B8%AD%E8%AF%91%E8%8B%B1_EN-US-2.png)

## Common Problems
### Time-consuming full data check task
#### Cause analysis
The DTS consistency check policy compares full data in the source and target TencentDB for MongoDB databases row by row. If the data volume is large, the check task may take longer and use more system resources, thus affecting the source service and migration task.

#### Solution
If the data volume is large and the check task is very slow, we recommend you stop the current task, manually create another consistency check task, and select **Row count check** as the data check method for quick comparison. Or, select **Content check** as the data check method and lower the proportion selected for **Sampling**, i.e., sampling a lower proportion of data for check. For detailed directions, see [Creating Data Consistency Check Task](https://cloud.tencent.com/document/product/240/81081).

- **Data Check**
  **Row count check**: It compares the number of rows of data in the source and target databases. 
  **Content check**: It compares the data content in the source and target databases row by row.
- **Sampling Percentage**: If you select **Content check**, you can sample a proportion of data for comparison.

![](https://staticintl.cloudcachetci.com/yehe/backend-news/SmEE014_31-en.png)

### Data inconsistency
#### Data content inconsistency
**Problem description**

**Cause analysis**
During a full data check, data is continuously written to the source database, and the oplog keeps being updated. The incremental data check task continuously reads the oplog from the source database. If the new oplog generated in the source database has not reached the timestamp in the target database, the data content may be inconsistent for a short period of time, which is normal.

**Solution**
You can check the inconsistent data row by row. You can also initiate a new check task to perform another manual check. When all the incremental data is migrated to the target database, the content will be consistent.

#### Data row count inconsistency
**Problem description**

**Cause 1**
During a full data check, data is continuously written to the source database, and the oplog keeps being updated. The incremental data check task continuously reads the oplog from the source database. If the new oplog generated in the source database has not reached the timestamp in the target database, the number of data rows may be inconsistent for a short period of time, which is normal.

**Cause 2**
The TencentDB for MongoDB row count check collects the row count in **metadata** through `db.collection.estimatedDocumentCount()` or `db.collection.stats()` for comparison, which may be inconsistent with the actual row count under specific circumstances such as unexpected instance shutdown or the presence of orphaned documents.

**Solution**
In this case, you can use `db.collection.countDocuments()` to compare the row count. Note that this requires collection scanning, which may affect the performance. For more information, see [db.collection.countDocuments()](https://www.mongodb.com/docs/v4.2/reference/method/db.collection.countDocuments/).

### Index check
**Problem**
If you select **Index** for **Database Info** when creating a consistency check task, the indexes in the source and target databases will be compared. You may find that the content of the `v` and `background` fields in the source and target databases are inconsistent, but the check result does not indicate any inconsistency.

**Cause analysis**
The TencentDB for MongoDB index check policy ignores the inconsistency in the `v` (version information) and `background` (creation in the background) fields, which will not be indicated in the check result.   

