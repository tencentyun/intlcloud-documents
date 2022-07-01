### The number of tables in a single instance exceeds 1 million

When the number of tables in a single instance exceeds 1 million, it may cause backup failure and affect database monitoring. You need to keep the number of tables in a single instance below 1 million.

### Large transactions caused by non-primary key tables

#### Cause

If there is no primary key table in the instance and the binlog is in row format, when a large amount of data is updated or deleted through a SQL statsment, playback on the slave machine will cause a large transaction, resulting in the backup thread unable to acquire the lock, resulting in backup failure.

#### Troubleshooting

1. Check all the non-primary key tables that exist in the instance through SQL statements.

```
select TABLE_SCHEMA,TABLE_NAME,TABLE_TYPE,ENGINE,TABLE_ROWS from information_schema.tables where (table_schema,table_name) not in (select table_schema,table_name from information_schema.columns where COLUMN_KEY='PRI') and table_schema not in ('sys','mysql','information_schema','performance_schema');
```

2. Add a primary key to a table without a primary key.

```
alter table table_name add primary key(`column_name`);
```
