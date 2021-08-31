### How do I set parameters to export data from TencentDB for MongoDB?
In mongodump parameters, set `--readPreference=secondaryPreferred`.

### What data migration types are supported in TencentDB for MongoDB?
Migration from CVM-based self-created and public network-based instances is supported. For more information, please see [TencentDB for MongoDB Data Migration](https://intl.cloud.tencent.com/document/product/240/8271).

### How do I export MongoDB data to my local device by using mongodump (for an entire database) or mongoexport (for a single collection)?

In CVM, you can use the MongoDB [shell client](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-linux/) to connect to TencentDB for MongoDB for data export. **Please use the latest MongoDB client suite.**
MongoDB provides two sets of official tools for data export. Generally, mongodump is used to export an entire database, where the BSON data format is used to facilitate massive data dump, while mongoexport is used to export a single collection, where the JSON data format is used for higher readability.
**1. Use mongodump to export an entire database for backup**
 The export command is as follows:

```
 mongodump --host 10.66.187.127:27017 -u mongouser -p thepasswordA1 --authenticationDatabase=admin --db=testdb -o /data/dump_testdb
```

![](https://main.qcloudimg.com/raw/0476329245feb3755334f10f0a4d3f5d.png)

**2. Use mongoexport to export a single collection for backup**
The export command is as follows:

```
mongoexport --host 10.66.187.127:27017 -u mongouser -p thepasswordA1 --authenticationDatabase=admin --db=testdb --collection=testcollection  -o /data/export_testdb_testcollection.json
```

>?In addition, you can include the `-f` parameter to specify a desired field or the `-q` parameter to specify a query condition so as to restrict the data to be exported.
>
**3. Parameters for export commands written by the users `rwuser` and `mongouser`** 
As described in the [Connection Sample](https://intl.cloud.tencent.com/document/product/240/7092), TencentDB for MongoDB provides two usernames `rwuser` and `mongouser` by default to support MONGODB-CR and SCRAM-SHA-1 authentication respectively.

- For `mongouser` and all new users created in the console, simply follow the above samples to use the export tools.
- For `rwuser`, the parameter `--authenticationMechanism=MONGODB-CR` should be included in each command.

mongodump sample:

```
 mongodump --host 10.66.187.127:27017 -u rwuser -p thepasswordA1 --authenticationDatabase=admin --authenticationMechanism=MONGODB-CR --db=testdb -o /data/dump_testdb
```

### How do I import local data into TencentDB for MongoDB by using mongorestore (for an entire database) or mongoimport (for a single collection)?

In CVM, you can use the MongoDB [shell client](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-linux/) to connect to TencentDB for MongoDB for data import. **Please use the latest MongoDB client suite.**
MongoDB provides two sets of official tools for data import. Generally, mongorestore is used to import an entire database, where the BSON data format is used to facilitate massive data mongorestore, while mongoimport is used to import a single collection, where the JSON data format is used for higher readability.    
**1. Use mongorestore to import an entire database for backup**
The import command is as follows:

```
mongorestore --host 10.66.187.127:27017 -u mongouser -p thepasswordA1 --authenticationDatabase=admin --dir=/data/dump_testdb
```

![](https://main.qcloudimg.com/raw/e1cea1fe2e2e73e4723a5de0472126c4.png)

**2. Use mongoimport to import a single collection for backup**
The import command is as follows:

```
mongoimport --host 10.66.187.127:27017 -u mongouser -p thepasswordA1 --authenticationDatabase=admin --db=testdb --collection=testcollection2  --file=/data/export_testdb_testcollection.json
```

**3. Parameters for import commands written by the users `rwuser` and `mongouser`**
As described in the [Connection Sample](https://intl.cloud.tencent.com/document/product/240/7092), TencentDB for MongoDB provides two usernames `rwuser` and `mongouser` by default to support MONGODB-CR and SCRAM-SHA-1 authentication respectively.

- For `mongouser` and all new users created in the console, simply follow the above samples to use the import tools.
- For `rwuser`, the parameter `--authenticationMechanism=MONGODB-CR` should be included in each command.

mongorestore sample:

```
 mongorestore --host 10.66.187.127:27017 -u rwuser -p thepasswordA1 --authenticationDatabase=admin --authenticationMechanism=MONGODB-CR --db=testdb -o /data/dump_testdb
```

### Why does the data imported into TencentDB for MongoDB occupy less capacity than in self-created MongoDB?

Possible causes:
- There are a large number of creation, deletion, and update operations accumulated after the database has been running for a long time.
- MongoDB allocates a larger capacity than the actual data size during write operations in order to improve performance.
- The original capacity is not reused after the data is deleted.
  All these result in an overall higher void rate in the entire database capacity. Meanwhile, importing data can be considered as an operation similar to disk defragging, which makes imported data more compact and appear smaller in size.

### What should I do if mongodump is unable to export data from MongoDB?
For more information on how to use mongodump, please see [Import and Export](https://intl.cloud.tencent.com/document/product/240/5321). You are recommended to use mongodump 3.2.10 or above.
