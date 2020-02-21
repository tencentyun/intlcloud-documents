You can restore data backup files into the target TencentDB for PostgreSQL instance by using PostgreSQL logical backup.


## 1. Prepare a PostgreSQL instance

Purchase a PostgreSQL instance, initialize it, and get its connection address.
> Please make sure that the character set for initialization is the same as that of the source instance.

## 2. Make a logical backup of the source instance data

Connect to the local (source) PostgreSQL database by using PostgreSQL client.

Run the following command to back up data.
```
pg_dump -U username -h hostname -p port databasename -f filename
```

Descriptions of parameters:

- username: username of the local database
- hostname: name of the local database server. You can use `localhost` if you log in from a local database server
- port: port number of the local database
- databasename: name of the local database to be backed up
- filename: name of the backup file to be generated

For example, if a database user named `pgtest` wants to back up a local PostgreSQL database, the user can log in to the PostgreSQL server and run the following command.

```
pg_dump -U pgtest -h localhost -p 4321 pg001 -f pg001.sql
```

## 3. Migrate data via CVM

You are recommended to upload data to a CVM instance in a secure way (such as encrypted compression) and restore data to the target PostgreSQL database over the private network.

Log in to CVM.

On the PostgreSQL client, run the following command to import data to the target PostgreSQL database.
```
psql -U username -h hostname -d desintationdb -p port -f dumpfilename.sql
```
Descriptions of parameters:

- username: username of the PostgreSQL database on RDS
- hostname: address of the PostgreSQL database on RDS
- port: port number of the PostgreSQL database on RDS
- databasename: name of the PostgreSQL database on RDS
- filename: filename of the local backup data.
Example:

psql -U pgtest -h 10.xxx.xxx.xxx -d pg001 -p 4321 -f pg001.sql
As the permission configuration of the source database may be different from that of the target database, some permission-related warnings or errors may appear during data import, which, however, can be ignored.

## 4. Migrate data over the internet
If the data volume is small (e.g., < 10 GB), you can also import it directly over the internet with tools such as pgAdmin.
