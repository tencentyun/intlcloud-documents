### How do I set parameters to export data from MongoDB?
In mongodump parameters, set --readPreference=secondaryPreferred.

### What of data migration types are supported by MongoDB?
Client's CVM instance migration and public network instance migration are supported. For more information, see [MongoDB Data Migration](https://cloud.tencent.com/document/product/240/8271).

### How do I export MongoDB data to my local device using mongodump (for the entire database) or mongoexport (for a single collection)?

In CVM, you can use the MongoDB [shell client](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-linux/) to connect with TencentDB for MongoDB for data export. **Please use the latest MongoDB client suite.**
MongoDB provides two sets of official tools for data export. Generally, mongodump is used to export the entire database. The data format, BSON, is used to facilitate massive data dump. While mongoexport is used to export a single collection. The data format, JSON, is used for higher readability.
**1. Use mongodump to export the entire database for backup**
 The export command is as follows:

```
 mongodump --host 10.66.187.127:27017 -u mongouser -p thepasswordA1 --authenticationDatabase=admin --db=testdb -o /data/dump_testdb
```

![](//bot1024-1253841380.file.myqcloud.com/598299decb2a1.png)

**2. Use mongoexport to export a single collection for backup**
The export command is as follows:

```
mongoexport --host 10.66.187.127:27017 -u mongouser -p thepasswordA1 --authenticationDatabase=admin --db=testdb --collection=testcollection  -o /data/export_testdb_testcollection.json
```

> ?In addition, you can include the "-f" parameter to specify a desired field, and "-q" to specify a query condition so as to restrict the data to be exported.

**3. Parameters for export commands written by the users rwuser and mongouser** 
As described in the [Connection Example](https://cloud.tencent.com/document/product/240/3563), TencentDB for MongoDB provides two user names rwuser and mongouser by default to support the MONGODB-CR and SCRAM-SHA-1 authentication respectively.

- For mongouser and all new users created in the console, simply follow the above examples to use the export tools.
- For rwuser, the parameter "--authenticationMechanism=MONGODB-CR" should be included in each command.

Example of mongodump:

```
 mongodump --host 10.66.187.127:27017 -u rwuser -p thepasswordA1 --authenticationDatabase=admin --authenticationMechanism=MONGODB-CR --db=testdb -o /data/dump_testdb
```

### How to import local data to MongoDB using mongorestore (for the entire database) or mongoimport (for a single collection)?

In CVM, you can use the MongoDB [shell client](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-linux/) to connect with TencentDB for MongoDB for data import. **Please use the latest MongoDB client suite.**
MongoDB provides two sets of official tools for data import. Generally, mongorestore is used to export the entire database. The data format, BSON, is used to facilitate massive data mongorestore. While mongoimport is used to export a single collection. The data format, JSON, is used for higher readability.    
**1. Use mongorestore to import the entire database for backup**
The import command is as follows:

```
mongorestore --host 10.66.187.127:27017 -u mongouser -p thepasswordA1 --authenticationDatabase=admin --dir=/data/dump_testdb
```

![](//bot1024-1253841380.file.myqcloud.com/5982b30189287.png)
**2. Use mongoimport to import a single collection for backup**
The import command is as follows:

```
mongoimport --host 10.66.187.127:27017 -u mongouser -p thepasswordA1 --authenticationDatabase=admin --db=testdb --collection=testcollection2  --file=/data/export_testdb_testcollection.json
```

**3. Parameters for import commands written by the users rwuser and mongouser**
As described in the [Connection Example](https://cloud.tencent.com/document/product/240/3563), TencentDB for MongoDB provides two user names rwuser and mongouser by default to support the MONGODB-CR and SCRAM-SHA-1 authentication respectively.

- For mongouser and all new users created in the console, simply follow the above examples to use the import tools.
- For rwuser, the parameter "--authenticationMechanism=MONGODB-CR" should be included in each command.

Example of mongorestore:

```
 mongorestore --host 10.66.187.127:27017 -u rwuser -p thepasswordA1 --authenticationDatabase=admin --authenticationMechanism=MONGODB-CR --db=testdb -o /data/dump_testdb
```

### Why does the data imported into TencentDB for MongoDB occupy less space than in client's MongoDB?

Here are the possible reasons:
- There are a large number of addition, deletion and modification operations accumulated after the database has been running for a long time.
- MongoDB allocates a larger space than the actual data size during write operations in order to improve performance.
- The original space is not reused after the data is deleted.
  All these result in an overall higher void rate in the entire database space. Meanwhile, importing data can be considered as an operation similar to disk defragging, which makes imported data more compact and appear smaller in size.

### What can I do if mongodump is unable to export data in MongoDB?
For information on how to use mongodump, see [Import and Export](https://cloud.tencent.com/document/product/240/5321). It is recommended to use mongodump 3.2.10 or above.

