## Check Details
If you select incremental migration as the migration type, you need to check the following conditions; otherwise, the verification will fail.
- The major version of the source and target databases need to be below PostgreSQL 10.x.
- `wal_level` in the source database must be set to `logical`.
- The `max_replication_slots` and `max_wal_senders` values in the target database must be greater than the total number of databases to be migrated.
- The `max_worker_processes` value in the target database must be greater than the `max_logical_replication_workers` value.
- The tables to be migrated should not include unlogged tables; otherwise, they cannot be migrated.

## Fix
If the version does not meet the requirements, you need to upgrade it. You can change the values of the `wal_level`, `max_replication_slots`, `max_worker_processes`, and `max_wal_senders` as follows:

1. Log in to the source database.
>?
>- If the source database is self-built, you need to log in to the server where the database runs and enter the main data directory of the database, which is usually `$PGDATA`.
>- If the source database is in another cloud, modify the parameters as requested by the corresponding cloud vendor.
>- If you need to modify the parameters in the target database, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
2. Open the `postgresql.conf` file and modify `wal_level`.
```
wal_level = logical
```
3. After the modification is completed, restart the database.
4. Log in to the database and run the following command to check whether the parameters are correctly set:
```
postgres=> select name,setting from pg_settings where name='wal_level';
   name    | setting 
-----------+---------
 wal_level | logical
(1 row)
postgres=> select name,setting from pg_settings where name='max_replication_slots';
         name          | setting 
-----------------------+---------
 max_replication_slots | 10
(1 row)
postgres=> select name,setting from pg_settings where name='max_wal_senders';
      name       | setting 
-----------------+---------
 max_wal_senders | 10
(1 row)
```
5. Run the verification task again.

