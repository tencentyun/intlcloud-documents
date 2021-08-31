Currently, you can import data backed up from `pg_dump` to PostgreSQL for Serverless through the `psql` command.

#### Directions
If your data is already in a self-built PostgreSQL database, you can use the `psql` command to easily migrate the data to PostgreSQL for Serverless.
The data migration is mainly divided into two steps:
1. Perform logical backup by using the `pg_dump` command to create dump data.
2. Restore the data backed up in the previous step to PostgreSQL for Serverless.

## Prerequisites
You have prepared a PostgreSQL for Serverless instance. If not, please see [Getting Started](https://intl.cloud.tencent.com/document/product/409/39715).

## Step 1. Export data
Connect to the local database by using the PostgreSQL client and run the following command to back up the data.
```
pg_dump -U username -h hostname -p port -O databasename -f filename
```
>?In order to avoid execution permission problems, you need to add the `-O` parameter.

| Parameter | Description |
| ------------ | ----------------------------------- |
| username     | Local database username                    |
| hostname     | Local database host name                    |
| port         | Local database port number                    |
| databasename | Name of the local database to be backed up                |
| filename     | Name of the backup file to be generated, such as mydump.sql |


## Step 2. Import data to PostgreSQL for Serverless
Preparations: upload the data backed up to a CVM instance in the same VPC as the PostgreSQL for Serverless instance, and then restore the data over the private network to ensure network stability and data security.

[Log in to the CVM instance](https://intl.cloud.tencent.com/zh/document/product/213/10517) and run the following command in the PostgreSQL client to restore the data.

```
psql -U username -h hostname -d desintationdb -p port -f dumpfilename
```

>?During the import, there may be some errors reported. You can find the specific causes according to the error messages. Some errors don't affect the data import.

| Parameter | Description |
| ------------- | ---------------------------------------- |
| username      | PostgreSQL for Serverless database username |
| hostname      | PostgreSQL for Serverless database address   |
| desintationdb | PostgreSQL for Serverless database name    |
| port          | PostgreSQL for Serverless database port number |
| dumpfilename  | Backup file name, such as mydump.sql            |
