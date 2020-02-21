## Using Tencent Cloud DTS
The **data migration** feature of Tencent Cloud **Data Transmission Service (DTS)** can be used to import data to TencentDB for PostgreSQL.

For more information, please see [Data Migration](https://cloud.tencent.com/document/product/571/16309).
 
## Using `psql` Command
If your data is already on PostgreSQL, you can easily migrate it to TencentDB for PostgreSQL by using the `psql` command.
Data migration mainly involves two parts:
>1. Perform logical backup by using the `pg_dump` command to create dump data.
>2. Restore the backup data to TencentDB for PostgreSQL.
Preparation: get the PostgreSQL instance ready. If not, please see the operation guide on applying for an instance and connecting to it.

### Step 1
Connect to the local database by using the PostgreSQL client and run the following command to back up the data.

```
pg_dump -U username -h hostname -p port -d databasename -f filename
```

Descriptions of parameters:


| Parameter | Description | 
|---------|---------|
| username | Username of the local database |
| hostname | Host name of the local database. You can use `localhost` if you log in from a local database host | 
| port | Port number of the local database | 
| databasename | Name of the local database to be backed up | 
| filename | Name of the backup file to be generated, such as `mydump.sql` | 


### Step 2
Preparation: upload the backup data to the CVM instance in the same private network and then restore the data over the private network, which helps ensure network stability and data security.
After you log in to the CVM instance, run the following command on the PostgreSQL client to restore the data.

```
psql -U username -h hostname -d desintationdb -p port -f dumpfilename
```
Descriptions of parameters:

| Parameter | Description  | 
|---------|---------|
| username | Username of a TencentDB for PostgreSQL database |
| hostname | Address of a TencentDB for PostgreSQL database | 
| desintationdb | Name of a TencentDB for PostgreSQL database | 
| port | Port number of a TencentDB for PostgreSQL database | 
| dumpfilename | Filename of the backup data, such as `mydump.sql` | 

