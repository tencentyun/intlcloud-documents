
In Tencent Cloud CVM, you can use the MongoDB shell client ([see the Installation Documentation](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-linux/)) to connect with TencentDB for MongoDB service for data management. Please use the latest version of MongoDB client suite.

### Quick start
A typical connection command is as follows:
```
mongo 10.66.187.127:27017/admin -u mongouser -p thepasswordA1
```
![](https://mc.qcloudimg.com/static/img/ce6b26f8cd6b1cc2981bc0cd44f9d09d/shell_default.png)

### Authentication methods for the connections
As described in the [Connection Example](https://cloud.tencent.com/doc/product/240/3563), By default, TencentDB for MongoDB provides two user names "rwuser" and "mongouser" for the "MONGODB-CR" and "SCRAM-SHA-1" authentication methods respectively.
Shell command parameters are different between these two authentication methods. See below for more information.

### SCRAM-SHA-1 authentication (mongouser)
**SCRAM-SHA-1 authentication is used by the default user "mongouser" and all new users created in the console.** Shell connection parameters are the same as those described in [Quick Start](#.E5.BF.AB.E9.80.9F.E5.BC.80.E5.A7.8B), without additional parameters. See the example below:
```
mongo 10.66.187.127:27017/admin -u mongouser -p thepasswordA1
```
Specifically, if you want to enter a "db" (“singer” in the example below) directly, after connecting with MongoDB, please proceed as described below:
```
mongo 10.66.187.127:27017/singer -u mongouser -p thepasswordA1 --authenticationDatabase admin
```

![](https://mc.qcloudimg.com/static/img/c30cc3e6e2db6c8bd3cce2e327ce63db/sha1_sonedb.png)

### MONGODB-CR authentication (rwuser)
**Please note that MONGODB-CR authentication can be used only by the default user "rwuser",** and the authentication method should be specified as MONGODB-CR in shell connection parameters. See the following example:
```
mongo 10.66.187.127:27017/admin -u rwuser -p thepasswordA1 --authenticationMechanism=MONGODB-CR
```

![](https://mc.qcloudimg.com/static/img/ff200b49c3fa5c70812027dd89e3ebc3/cr_default.png)
Specifically, if you want to enter a "db" (“singer” in the example below) directly after connecting to MongoDB, please proceed as described below:
```
mongo 10.66.187.127:27017/singer -u rwuser -p thepasswordA1 --authenticationMechanism=MONGODB-CR --authenticationDatabase admin
```

![](https://mc.qcloudimg.com/static/img/d31bfa612a295fd070ea5dd09c7ce6a3/cr_somedb.png)

### Import and export data using shell
You can use Shell to import and export data both authentication methods described in this document. [See Here](https://cloud.tencent.com/doc/product/240/5321).

