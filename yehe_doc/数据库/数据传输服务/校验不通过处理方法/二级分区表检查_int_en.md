## TDSQL for MySQL Check Details

- If the source database is TDSQL for MySQL, the migration task will report a warning if there are level-2 subpartitioned tables. You can ignore the warning and continue with the task, in which case the level-2 subpartitioned tables will be skipped for migration. If there are such tables in a data sync task, the verification will fail, and you need to remove these tables. For more information, see [Subpartitioning](https://cloud.tencent.com/document/product/557/58907).
- As the underlying logic of level-2 subpartitioned tables is implemented based on subtables, the target database will report an exception when level-2 subpartitioned tables are migrated or synced.

## Troubleshooting

Remove the level-2 subpartitioned tables from the list of tables to be migrated or synced.

