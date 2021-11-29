This document describes how to use DTS or PostgreSQL logical backups to restore data backup files to a TencentDB for PostgreSQL instance.

## DTS
For detailed data migration solutions, see [Migration from PostgreSQL to TencentDB for PostgreSQL](https://intl.cloud.tencent.com/document/product/571/42640). Currently, you can migrate many types of PostgreSQL databases to TencentDB for PostgreSQL.

## Data Import/Export
### Step 1. Prepare a TencentDB for PostgreSQL instance
[Purchase a TencentDB for PostgreSQL instance](https://intl.cloud.tencent.com/document/product/409/40724) and get its connection address in the [console](https://console.cloud.tencent.com/postgres).
>?Make sure that its character set is the same as that of the source instance.

### Step 2. Make a logical backup of the source instance
1. Connect to the local (source) PostgreSQL database using a PostgreSQL client.
2. Run the following command to back up data:
```
pg_dump -U username -h hostname -p port -x databasename -f filename
```
The parameters are described as follows:
- username: username of the local database.
- hostname: hostname of the local database server. You can use "localhost" if you're logging in from the local database server.
- port: port number of the local database.
- databasename: name of the local database to be exported.
- filename: name of the generated backup file.
- -x: export data without object permission information of the source database. Importing data with permission information is prone to error. We recommend that you grant permissions later in the target database as needed.

For example, if a database user named `pgtest` wants to back up a local PostgreSQL database, the user can log in to the PostgreSQL server and run the following command:
```
pg_dump -U pgtest -h localhost -p 4321 pg001 -f pg001.sql
```

### Step 3. Restore data to the target instance
We recommend that you upload data to a CVM instance in a secure way (such as encryption and compression) and restore data to the target TencentDB for PostgreSQL instance over the private network.

1. Log in to the CVM instance.
2. On the PostgreSQL client, run the following command to import data to the target TencentDB for PostgreSQL instance:
```
psql -U username -h hostname -d databasename -p port -f filename
```

The parameters are described as follows:
- username: database username of the target TencentDB for PostgreSQL instance
- hostname: connection address of the target TencentDB for PostgreSQL instance
- port: port number of the target TencentDB for PostgreSQL instance
- databasename: database name of the target TencentDB for PostgreSQL instance
- filename: name of the local backup file

For example:
```
psql -U pgtest -h 10.xxx.xxx.xxx -d pg001 -p 4321 -f pg001.sql
```
Because the permission configuration of the source database may be different from that of the target database, permission-related warnings or errors may appear during the data import process, which can be ignored.
