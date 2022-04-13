
## Issue Description
Failed to enable case insensitivity. An error was reported as follows:
![](https://main.qcloudimg.com/raw/e10049c280384344318379432bc294fb.png)
>?If the database version is 8.0, you can only choose whether to enable case sensitivity for table names when creating an instance on the purchase page. You cannot modify the `lower_case_table_names` parameter after creating the instance.

## Common Causes
Database or table names contain uppercase letters.

## Troubleshooting
Check whether all of the database and table names of the instance are lowercase, convert uppercase names (if any) to lowercase ones, and modify the `lower_case_table_names` parameter.
>!Modifying `lower_case_table_names` will cause the database restart.
>
- Check if there are uppercase table names
```
select table_schema,table_name from information_schema.tables where   table_schema not in("mysql","information_schema") and (md5(table_name)<>md5(lower(table_name)) or md5(table_schema)<>md5(lower(table_schema)));
```
- Check if there are uppercase database names
```
select SCHEMA_NAME from information_schema.SCHEMATA where md5(SCHEMA_NAME)<>md5(lower(SCHEMA_NAME));
```

