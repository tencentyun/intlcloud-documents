
## MySQL/TDSQL-C Check Details
- Foreign key dependency can only be set to `NO ACTION`, `RESTRICT`, or `CASCADE`.
- During partial table migration, tables with foreign key dependency must be migrated.

## TDSQL for MySQL Check Details

- Foreign key dependency can only be set to only `NO ACTION` or `RESTRICT`.
- During partial table migration, tables with foreign key dependency must be migrated.

## Fix

### Modifying foreign key rule
When you set a foreign key in MySQL, there are four values can be selected for the `ON DELETE` and `ON UPDATE` columns: 
- `CASCADE`: when a record is deleted or updated in the parent table, its associated records will also be deleted or updated in the child table.
- `SET NULL`: when a record is deleted or updated in the parent table, the column of the foreign key field of its associated records will be set to `null` in the child table (child table foreign keys cannot be set to `not null`).
- `RESTRICT`: when a record is deleted or updated in the parent table, if it is associated with records in the child table, the deletion request in the parent table will be denied.
- `NO ACTION`: similar to `RESTRICT`, the foreign key will be checked first.

If an error occurs, fix it as follows:
#### Windows
1. [Log in to the DMC platform in the source database](https://intl.cloud.tencent.com/document/product/236/39353).
2. Select the table to be modified in the target tree on the left and click the **Foreign Key** tab on the opened table editing page to modify the foreign key parameter as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/9671fd44db2250287d7e81564637f01f.png)
3. After completing the modification, click **Save**.
4. Run the verification task again.

#### Linux
1. [Log in to the source database](https://intl.cloud.tencent.com/document/product/236/37788).
2. Delete the original foreign key settings.
```
alter table `table name 1` drop foreign key `foreign key name 1`;
```
3. Add the foreign key settings again.
```
alter table `table name 1` add constraint `foreign key name 2` foreign key `table name 1`(`column name 1`) references `table name 2`(`column name 1`)
on delete cascade on update cascade;
```
4. Run the verification task again.

### Completing migration object
When modifying the migration task configuration, include objects with associations in migration objects.
1. Log in to the [DTS console](https://console.cloud.tencent.com/dts/migration), select the corresponding migration task, and click **More** > **Modify** in the **Operation** column. 
2. Check the objects with associations in the **Migration Object**.
3. Run the verification task again. 

