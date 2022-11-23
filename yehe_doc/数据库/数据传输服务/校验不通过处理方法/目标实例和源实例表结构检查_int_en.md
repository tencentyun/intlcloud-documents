## TDSQL for MySQL Check Details

- If the target database is TDSQL for MySQL, we recommend you create a partitioned table and specify a shardkey in the target database in advance; otherwise, the task will report a warning. You can ignore the warning and continue with the task. After the warning is ignored, DTS will create a table in the target database based on the source database table paradigm. If the source database is a standalone instance, DTS will create a single table.
- If you have already created a partitioned table in the target database or don’t need one, DTS will check whether the source and target database table structures are consistent. The verification will fail if the field types, field names, or encoding methods are inconsistent.

## Troubleshooting

When the verification fails, DTS will display the list of tables with inconsistent table structures. You can modify the target table structure based on the inconsistencies.

