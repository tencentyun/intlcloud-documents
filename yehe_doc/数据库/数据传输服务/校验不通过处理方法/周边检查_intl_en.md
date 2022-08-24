
## MySQL/TDSQL for MySQL/TDSQL-C check details
- Check requirements: The `innodb_stats_on_metadata` environment variable in the source database must be set to `OFF`. 
-- Check description:
   - If the `innodb_stats_on_metadata` parameter is enabled, every time tables in the `information_schema` metadatabase are queried, InnoDB will update the `information_schema.statistics` table, causing slower access. After this parameter is disabled, access to the schema table can be faster.
   - On MySQL versions earlier than 5.6.6, the default value of the `innodb_stats_on_metadata` parameter is `ON`, and you need to change it to `OFF`. On MySQL 5.6.6 or later, the default value is `OFF`, which has no problem.

## TDSQL for PostgreSQL check details
The `wal_level` of the DN node must be logical.

## Troubleshooting
1. Log in to the source database.
2. Change the value of `innodb_stats_on_metadata` to `OFF`.
```
set global innodb_stats_on_metadata = OFF;
```
3. Check whether the configuration takes effect.
```
show global variables like '%innodb_stats_on_metadata%';
```
The system should display a result similar to the following:
```
mysql> show global variables like '%innodb_stats_on_metadata%';
+--------------------------+-------+
| Variable_name            | Value |
+--------------------------+-------+
| innodb_stats_on_metadata | OFF   |
+--------------------------+-------+
1 row in set (0.00 sec)
```
4. Run the verification task again.

