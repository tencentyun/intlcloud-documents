This document describes how to restore logical backup data to a TencentDB for PostgreSQL instance.

## Step 1. Prepare a TencentDB for PostgreSQL instance
[Purchase a TencentDB for PostgreSQL instance](https://intl.cloud.tencent.com/document/product/409/40724) and get its connection address.
>?Make sure that its character set is the same as that of the source instance.

## Step 2. Make a logical backup of the source instance
1. Connect to the local (source) PostgreSQL database using a PostgreSQL client.
2. Run the following command to back up data:

```
pg_dump -U username -h hostname -p port databasename -f filename
```
The parameters are described as follows:
- username: username of the local database.
- hostname: hostname of the local database server. You can use "localhost" if you're logging in from the local database server.
- port: port number of the local database.
- databasename: name of the local database to be backed up.
- filename: name of the generated backup file.

For example, if a database user named `pgtest` wants to back up a local PostgreSQL database, the user can log in to the PostgreSQL server and run the following command:
```
pg_dump -U pgtest -h localhost -p 4321 pg001 -f pg001.sql
```

## Step 3. Restore data to the target instance
### Migrating data through CVM
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

### Migrating data over the internet
If the data volume is small (e.g., less than 10 GB), you can use tools such as pgAdmin to access the public network address of the target instance and import data to it over the internet.

