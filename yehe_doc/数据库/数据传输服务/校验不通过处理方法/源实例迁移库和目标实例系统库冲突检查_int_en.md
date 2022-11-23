## TDSQL for MySQL Check Details

- If the target database is TDSQL for MySQL and the database named `sysdb` is included in the databases to be migrated, it won’t be migrated.
- Note: `sysdb` is the system database in TDSQL for MySQL. If a database to be migrated is named `sysdb`, the migration task will report a warning but continue to run normally.

## Troubleshooting

Remove `sysdb` from the list of databases to be migrated.

