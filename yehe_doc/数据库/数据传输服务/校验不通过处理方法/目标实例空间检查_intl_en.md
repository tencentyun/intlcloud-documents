
## Check Details
#### MySQL/TDSQL-C for MySQL/TDSQL for MySQL/PostgreSQL check requirements

The storage space of the target database must be at least 1.2 times the size of the tables to be migrated in the source database.
Full data migration will execute INSERT operations concurrently, generating data fragments in some tables of the target database. Therefore, after full migration is completed, the size of the tables in the target database may be larger than that in the source instance.

#### MongoDB check requirements
The storage space of the target database must be at least 1.3 times the size of the tables to be migrated in the source database.

#### Redis check requirements

The storage space of the target database must be at least 1.5 times that of the source database.

## Troubleshooting
- Delete some data from the target database to free up sufficient space. 
- Upgrade the storage specification of the target database as instructed in [Adjusting Database Instance Specification](https://intl.cloud.tencent.com/document/product/236/19707) to use an instance with a larger capacity for migration.

