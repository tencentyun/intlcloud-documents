
## MySQL/TDSQL for MySQL check details 
- Check requirements: The target database version must be later than or equal to the source database version, and all versions in migration and sync tasks must meet the version requirements.
- Check description: Here, the versions are differentiated by the major version number; for example, v5.6.x supports migration or sync to v5.6.x, v5.7.x, and later. The last digit is the minor version number, which is not restricted; for example, v5.6.5 can be migrated or synced to v5.6.4, but there may be compatibility issues.

## PostgreSQL check details
- Versions earlier than PostgreSQL 10.x (such as 9.x) do not support full + incremental migration. If an incremental migration task is configured for the source database, the verification will fail.
- If the versions are different, some special compatibility issues may arise, and a warning will appear during migration. Read the compatibility report for each version to check whether your business is using any incompatible features.

## TDSQL for PostgreSQL check details

Log in to the database, run `select tbase_version();`, and `Tbase_V2.xx` must be returned.

## MongoDB check details
The source and target database versions must be supported by MongoDB.

## SQL Server check details

Only migration from Basic Edition to High Availability Edition (including Dual-Server High Availability Edition and Cluster Edition) is supported, and the version number of the target instance must be later than that of the source instance. 

## Redis check details

- The source Redis instance must be on v2.2.6 or later. Earlier versions don't support migration through DTS.
- The target database version must be later than or equal to the source database version; otherwise, an alarm will be triggered for compatibility problems during verification.
- The proxy of the target Redis database must be on the latest version. 

## Troubleshooting
Check the source and target databases as instructed in [Databases Supported for Data Migration](https://intl.cloud.tencent.com/document/product/571/42647) and [Databases Supported for Data Sync](https://intl.cloud.tencent.com/document/product/571/42579). If the source or target database version is not supported, upgrade the target instance version or use a database instance on a later version.

