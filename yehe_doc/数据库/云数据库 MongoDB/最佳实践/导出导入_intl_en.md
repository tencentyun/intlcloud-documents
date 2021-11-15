
On a CVM instance, you can use the MongoDB shell client to connect to TencentDB for MongoDB for data import and export. Please be sure to use the latest MongoDB client suite. For detailed directions, please see [Access Connection > Connection Samples](https://intl.cloud.tencent.com/document/product/240/7092).
>!The `local` database mainly stores metadata such as configuration information of the replica set and oplog, and the `admin` database mainly stores information such as users and roles. In order to prevent data disorder and authentication failures, TencentDB for MongoDB prohibits importing `local` and `admin` databases into an instance.

## Export and Import Commands
MongoDB provides two sets of official tools for data import and export:
- mongodump and mongorestore 
- mongoexport and mongoimport

### mongodump and mongorestore
[mongodump](https://docs.mongodb.com/manual/reference/program/mongodump/) and [mongorestore](https://docs.mongodb.com/manual/reference/program/mongorestore/) are generally used to export and import an entire database, as they manipulate data in BSON format, which is more efficient when a large number of `dump` and `restore` operations are performed.

- The export command for mongodump is as follows:
```
mongodump --host 10.66.187.127:27017 -u mongouser -p thepasswordA1 --authenticationDatabase=admin --db=testdb -o /data/dump_testdb
```
The command is executed successfully, if the following information is output:
![](https://mc.qcloudimg.com/static/img/4071cfd5d9b54c720349f41fc2e07b0c/dump_default.png)
- The import command for mongorestore is as follows:
```
mongorestore --host 10.66.187.127:27017 -u mongouser -p thepasswordA1 --authenticationDatabase=admin --dir=/data/dump_testdb
```
The command is executed successfully, if the following information is output:
![](https://mc.qcloudimg.com/static/img/335dbef8f11a5417e42740472df1a5b8/restore_default.png)

### mongoexport and mongoimport
[mongoexport](https://docs.mongodb.com/manual/reference/program/mongoexport/) and [mongoimport](https://docs.mongodb.com/manual/reference/program/mongoimport/) are generally used to export and import a single set, as they manipulate data in JSON format, which features a higher readability.

- The export command for mongoexport is as follows:
```
mongoexport --host 10.66.187.127:27017 -u mongouser -p thepasswordA1 --authenticationDatabase=admin --db=testdb --collection=testcollection -o /data/export_testdb_testcollection.json
```
In addition, you can also include the `-f` parameter to specify a desired field or the `-q` parameter to specify a query condition so as to restrict the data to be exported.
- The import command for mongoimport is as follows:
```
mongoimport --host 10.66.187.127:27017 -u mongouser -p thepasswordA1 --authenticationDatabase=admin --db=testdb --collection=testcollection2 --file=/data/export_testdb_testcollection.json
```

## Authentication Methods and Parameters
As described in [Access Connection > Connection Samples](https://intl.cloud.tencent.com/zh/document/product/240/7092), TencentDB for MongoDB provides two usernames `rwuser` and `mongouser` by default to support the `MONGODB-CR` and `SCRAM-SHA-1` authentication methods, respectively.
- For `mongouser` and all new users created in the console, follow the above directions to use the import and export tools.
- For `rwuser`, the parameter `--authenticationMechanism=MONGODB-CR` should be included in each command.

Sample of mongodump:
```
mongodump --host 10.66.187.127:27017 -u rwuser -p thepasswordA1 --authenticationDatabase=admin --authenticationMechanism=MONGODB-CR --db=testdb -o /data/dump_testdb
```
