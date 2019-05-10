>!The local database store stores metadata of a replica set, including configuration information and oplog. The admin database manages information about users and roles. To prevent data corruption, authentication failure and other issues, TencentDB for MongoDB does not allow to import local and admin databases into instances.

In CVM, you can use the MongoDB shell client to connect to TencentDB for MongoDB service for data import and export. Please use the latest MongoDB client suite. For more information, see [**Operation Guide** -> **Connection Example**](https://cloud.tencent.com/document/product/240/3563).

## Import Commands
#### mongodump and mongorestore

MongoDB provides two sets of data import and export tools. If you need to import and export the entire database, we recommend [mongodump](https://docs.mongodb.com/manual/reference/program/mongodump/) and [mongorestore](https://docs.mongodb.com/manual/reference/program/mongorestore/). The data should be formatted in BSON, which facilitates massive data "dump" and "restore".
The mongodump import command is as follows:
```
mongodump --host 10.66.187.127:27017 -u mongouser -p thepasswordA1 --authenticationDatabase=admin --db=testdb -o /data/dump_testdb
```

![](https://mc.qcloudimg.com/static/img/4071cfd5d9b54c720349f41fc2e07b0c/dump_default.png)
The mongorestore import command is as follows:
```
mongorestore --host 10.66.187.127:27017 -u mongouser -p thepasswordA1 --authenticationDatabase=admin --dir=/data/dump_testdb
```

![](https://mc.qcloudimg.com/static/img/335dbef8f11a5417e42740472df1a5b8/restore_default.png)

## Export Commands
#### mongoexport and mongoimport

When you import and export a single collection, we recommend [mongoexport](https://docs.mongodb.com/manual/reference/program/mongoexport/) and [mongoimport](https://docs.mongodb.com/manual/reference/program/mongoimport/) . The data should be in JSON format for higher readability.

The mongoexport export command is as follows:

```
mongoexport --host 10.66.187.127:27017 -u mongouser -p thepasswordA1 --authenticationDatabase=admin --db=testdb --collection=testcollection -o /data/export_testdb_testcollection.json
```

In addition, you can add the "-f" into the parameter to specify a desired field, and "-q" to specify a query condition that applies restriction on data export.
The mongoimport export command is as follows:

```
mongoimport --host 10.66.187.127:27017 -u mongouser -p thepasswordA1 --authenticationDatabase=admin --db=testdb --collection=testcollection2 --file=/data/export_testdb_testcollection.json
```

## Parameters of Authentication Methods

As described in the [Connection Example](https://cloud.tencent.com/doc/product/240/3563), TencentDB for MongoDB provides two user names "rwuser" and "mongouser" by default to support the "MONGODB-CR" and "SCRAM-SHA-1" authentication respectively.
- For "mongouser" and all new users created in the console, they can simply follow the example above to use the import and export tools.
- For "rwuser", the parameter "--authenticationMechanism=MONGODB-CR" should be included in each command.

Example of mongodump:
```
mongodump --host 10.66.187.127:27017 -u rwuser -p thepasswordA1 --authenticationDatabase=admin --authenticationMechanism=MONGODB-CR --db=testdb -o /data/dump_testdb
```




