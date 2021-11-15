## Check Details

### MySQL/TDSQL-C for MySQL/TDSQL for MySQL/PostgreSQL check requirements

- The target database cannot have objects with the same name as those in the source database. If a conflict causes an error, you can fix it in one of the following methods:
   - [Method 1: use database/table mapping (for MySQL only)](#1). 
   - [Method 2: rename or delete objects with the same name in the target database](#2).
   - [Method 3: remove objects with the same name from the migration objects](#3).
- The target database must be empty. If a conflict causes an error, you need to delete the database content.

### MongoDB check requirements

The target database can have tables with the same name as those in the source database, but they must be empty tables. If a conflict causes an error, you can fix it in one of the following methods:

- Method 1: delete tables with the same name in the target database or clear their data.
- [Method 2: remove objects with the same name from the migration objects](#3).

### SQL Server check requirements

The target database cannot have databases with the same name as those in the source database; otherwise, an error will be reported.

If an error is reported, you need to delete or rename databases with the same name from the target database.

## Fix

### [Using table mapping (for MySQL only)](id:1)
You can use the DTS table mapping feature to map the names of the objects to be migrated with the same name to other names in the target database. 
1. Log in to the [DTS console](https://console.cloud.tencent.com/dts/migration), select the corresponding migration task, and click **More** > **Modify** in the **Operation** column. 
2. In **Selected Object** on the right, hover over an object to be modified, click the displayed **Edit** icon, and rename the object.
![](https://qcloudimg.tencent-cloud.cn/raw/c89be2f80c4c4c7bc53858cb8bc24ccc.png)
3. Run the verification task again.

### [Modifying objects with the same name in target database](id:2)
Log in to the target database, rename or delete the objects with the same name as the migration objects.

### [Removing objects with the same name from migration objects](id:3)
Modify the migration task configuration to remove the objects with the same name from the migration objects. The removed objects cannot be migrated.
1. Log in to the [DTS console](https://console.cloud.tencent.com/dts/migration), select the corresponding migration task, and click **More** > **Modify** in the **Operation** column. 
2. Remove the objects with the same name from the migration objects.
3. Run the verification task again. 

### Deleting target database content
Log in to the target database, delete the objects with the same name as those in the source database, and run the verification task again.

