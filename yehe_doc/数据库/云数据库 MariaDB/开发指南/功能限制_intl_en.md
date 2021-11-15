
1. You cannot change any data in the `mysql`, `information_schema`, `performance_schema`, or `sysdb` database.

2. SQL statements cannot be directly used to set accounts or grant permissions, which can only be done in the console.
The following 19 common permissions are supported, and only few rarely used permissions are not supported:
SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, REFERENCES, INDEX, ALTER
CREATE TEMPORARY TABLES, LOCK TABLES, EXECUTE, CREATE VIEW, SHOW VIEW
CREATE ROUTINE, ALTER ROUTINE, EVENT, TRIGGER, SHOW DATABASES

3. No root account is provided.

4. You are recommended to use the [InnoDB storage engine](https://intl.cloud.tencent.com/document/product/237/5276).
