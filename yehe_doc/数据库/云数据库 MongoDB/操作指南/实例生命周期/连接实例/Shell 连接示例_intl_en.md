
You can use the MongoDB shell client (please see the [installation documentation](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-linux/)) on a CVM instance to connect to TencentDB for MongoDB for data management. Be sure to use the latest version of MongoDB client suite.

### Quick start
A typical connection command is as follows:
```
mongo 10.66.187.127:27017/admin -u mongouser -p thepasswordA1
```
>!To access TencentDB for MongoDB via a connection string, special characters in the password need to be converted to URL encoded characters so that they can be correctly identified. For example, "@" should be converted to "%40".
>
See the figure below:
![](https://mc.qcloudimg.com/static/img/ce6b26f8cd6b1cc2981bc0cd44f9d09d/shell_default.png)

### Connection in different authentication methods
As described in the [Connection Sample](https://intl.cloud.tencent.com/document/product/240/7092), TencentDB for MongoDB provides two usernames `rwuser` and `mongouser` by default to support the MONGODB-CR and SCRAM-SHA-1 authentication methods, respectively.
For those two authentication methods, the shell parameters are not the same. See below for more information.

### SCRAM-SHA-1 authentication (mongouser)
**SCRAM-SHA-1 authentication is used for the default user `mongouser` and all new users created in the console.** Shell connection parameters are the same as those described in [Quick Start](#.E5.BF.AB.E9.80.9F.E5.BC.80.E5.A7.8B) without additional parameters required. See the example below:
```
mongo 10.66.187.127:27017/admin -u mongouser -p thepasswordA1
```
If you want to enter a specific `db` directly such as "singer", after connecting to MongoDB, proceed as described below:
```
mongo 10.66.187.127:27017/singer -u mongouser -p thepasswordA1 --authenticationDatabase admin
```
See the figure below:
![](https://mc.qcloudimg.com/static/img/c30cc3e6e2db6c8bd3cce2e327ce63db/sha1_sonedb.png)

### MONGODB-CR authentication (rwuser)
**Please note that MONGODB-CR authentication is used only for the default user `rwuser`**, and the authentication method of MONGODB-CR should be expressly specified in the shell connection parameters. See the example below:
```
mongo 10.66.187.127:27017/admin -u rwuser -p thepasswordA1 --authenticationMechanism=MONGODB-CR
```
See the figure below:
![](https://mc.qcloudimg.com/static/img/ff200b49c3fa5c70812027dd89e3ebc3/cr_default.png)
If you want to enter a specific `db` directly such as "singer", after connecting to MongoDB, proceed as described below:
```
mongo 10.66.187.127:27017/singer -u rwuser -p thepasswordA1 --authenticationMechanism=MONGODB-CR --authenticationDatabase admin
```
See the figure below:
![](https://mc.qcloudimg.com/static/img/d31bfa612a295fd070ea5dd09c7ce6a3/cr_somedb.png)

### Using shell to import and export data
For both authentication methods, you can use the shell to import and export data. For more information, please see [Export and Import](https://intl.cloud.tencent.com/document/product/240/5321).

