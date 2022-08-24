
## Check details
Check whether you have the operation permissions of the database by referring to the following documents:

- Permission requirements for data migration

   - [Migration from MySQL to TencentDB for MySQL](https://intl.cloud.tencent.com/document/product/571/42645)
   - [Migration from TDSQL for MySQL to TDSQL for MySQL](https://intl.cloud.tencent.com/document/product/571/47366)
   -  [Migration from PostgreSQL to TencentDB for PostgreSQL](https://intl.cloud.tencent.com/document/product/571/42640)
   -  [Migration from MongoDB to TencentDB for MongoDB](https://intl.cloud.tencent.com/document/product/571/42639)
   -  [Migration from SQL Server to TencentDB for SQL Server](https://intl.cloud.tencent.com/document/product/571/42638)

- Permission requirements for data sync
   - [Sync from MySQL/MariaDB/Percona to TencentDB for MySQL](https://intl.cloud.tencent.com/document/product/571/47344)
   - [Sync from TDSQL for MySQL to TDSQL for MySQL](https://intl.cloud.tencent.com/document/product/571/47350)


- Permission requirements for data subscription
   - [Creating TencentDB for MySQL or TDSQL-C for MySQL Data Subscription](https://intl.cloud.tencent.com/document/product/571/47354)    
   - [Creating TDSQL for PostgreSQL Data Subscription](https://intl.cloud.tencent.com/document/product/571/47357)   

## TDSQL for PostgreSQL check details
You must have the REPLICATION permission, i.e., `pg_roles.rolreplication`.

You must have the SELECT permission of the subscribed table. For entire database subscription, you must have the SELECT permission of all the tables under the schema.

## Troubleshooting

If you don't have the operation permissions, get authorized based on the permission requirements in the check details and run the verification task again.

