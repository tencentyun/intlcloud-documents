
## Check Details
- Check requirements:
   - MySQL/TDSQL-C for MySQL/TDSQL for MySQL/PostgreSQL: the storage space of the target database needs to be at least 1.2 times the size of the tables to be migrated in the source database.
   - MongoDB: the storage space of the target database needs to be at least 1.3 times the size of the tables to be migrated in the source database.
- Check description: full data migration will execute INSERT operations concurrently, generating data fragments in some tables of the target database. Therefore, after full migration is completed, the size of the tables in the target database may be larger than that in the source database.

## Fix
- Delete some data from the target database to free up sufficient space. 
- [Upgrade the storage specification of the target database](https://intl.cloud.tencent.com/document/product/236/19707) to use an instance with a larger capacity for migration.

