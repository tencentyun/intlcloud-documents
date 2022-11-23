## TDSQL for MySQL/MariaDB Check Details

If the target database is TDSQL for MySQL or TencentDB for MariaDB, only InnoDB tables can be migrated or synced. If the objects to be migrated or synced include non-InnoDB tables, the verification will fail.

## Troubleshooting

Remove non-InnoDB tables as prompted and execute the verification task again.
