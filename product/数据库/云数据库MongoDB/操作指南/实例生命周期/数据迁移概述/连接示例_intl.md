After initializing the instance, you can use either MongoDB shell or drivers in different languages to access the database to perform administrative operations. Using CVM, you can only access the database through the private network, instead of the public network.

## Description
### Client version
A driver with version 3.2 or above is required to connect to the TencentDB for MongoDB service. Please use the **latest version** of the client driver, including shell kit, java jar package, php expansion, nodejs module, to ensure the best compatibility. For more information, see [MongoDB Drivers](https://docs.mongodb.com/ecosystem/drivers/).
### Use mongo shell to connect to MongoDB
The mongo shell is an interactive JavaScript interface to MongoDB. You can use the mongo shell to query and update data as well as perform administrative operations. The mongo shell is a component of the MongoDB distributions. Once you have installed and have started MongoDB, connect the mongo shell to your running MongoDB instance. Download a MongoDB distribution here [link](https://www.mongodb.com/download-center#community). 

The example below describes how to start the mongo Shell and connect to MongoDB:
```
    cd <mongodb installation dir>
	./bin/mongo -umongouser -plxh2081* 172.16.0.56:27017/admin
```
 > In the above example, "-u" indicates the user name, "-p" indicates the password, “172.16.0.56” is the IP, and 27017 is the default port of the MongoDB instance.

### Use connection String URI to connect to MongoDB
The MongoDB service can be connected by passing parameters, and most drivers can also be connected by using URI. Connection to the MongoDB service using URI is officially recommended by MongoDB.  You can specify URI to define the connections between most of the applications and MongoDB instances in the official MongoDB drivers. MongoDB recommends you use connection string URI. 

Below are examples of URIs:

Example 1
```
mongodb://username:password@IP:27017/admin
```
Example 2
```
mongodb://username:password@IP:27017/somedb?authSource=admin
```
Example 3
```
mongodb://username:password@IP:27017/somedb?authSource=admin&readPreference=secondaryPreferred
```

The parameters in URI are described as follows:

| Parameter | Description | Required |
|---------|---------|---------|
| mongodb:// | A specific string indicating MognoDB protocol | Yes |
| username | The user name used to log in to the MongoDB service | Yes. See "[Default users](#.E9.BB.98.E8.AE.A4.E7.94.A8.E6.88.B7.E5.90.8D)" on this page. |
| password | The user password used to log in to the MongoDB service | Yes |
| IP:27017 | IP and port of the MongoDB service | Yes |
| /admin | The database to be authenticated. TencentDB for MongoDB is always admin. | Yes. See "[Authentication database](#.E8.AE.A4.E8.AF.81.E6.95.B0.E6.8D.AE.E5.BA.93)" on this page. |
| authMechanism=MONGODB-CR | Authentication method | See "[Authentication mechanism](#.E8.AE.A4.E8.AF.81.E6.9C.BA.E5.88.B6)" on this page. |
| authSource=admin | The database for authentication. TencentDB for MongoDB is always admin. | Yes. See "[Authentication database](#.E8.AE.A4.E8.AF.81.E6.95.B0.E6.8D.AE.E5.BA.93)" on this page. |
| readPreference=secondaryPreferred | You can decide whether the slave has higher read priority | No. See "[Master/Slave Read Priority](#.E8.AF.BB.E6.93.8D.E4.BD.9C.E7.9A.84.E4.B8.BB.E4.BB.8E.E4.BC.98.E5.85.88.E7.BA.A7)" on this page. |
Only some of the parameters for the connection string URI are listed here. For more information, see [MongoDB official reference documentation](https://docs.mongodb.com/manual/reference/connection-string/).

### Default users

The default users vary by the version of TencentDB for MongoDB. For the latest instances, The built-in default users are  "rwuser" and "mongouser". For older instances, the default user is "rwuser" (we will upgrade these old instances, and contact you before the upgrade). You can also use TencentDB for MongoDB Console to manage account and permission to meet your business requirements.

#### Example of rwuser (MONGODB-CR authentication) URI
**MONGODB-CR authentication is used by rwuser only.**
```
mongodb://rwuser:password@10.66.100.186:27017/admin?authMechanism=MONGODB-CR
or
mongodb://rwuser:password@10.66.100.186:27017/somedb?authMechanism=MONGODB-CR&authSource=admin
```

#### Example of mongouser (SCRAM-SHA-1 authentication) URI
**SCRAM-SHA-1 authentication is used by mongouser and users created in the console.**
```
mongodb://mongouser:password@10.66.100.186:27017/admin
or
mongodb://mongouser:password@10.66.100.186:27017/somedb?authSource=admin
```

### Authentication database
TencentDB for MongoDB uses "admin" database as the authentication database for login authentication, so the port in the URI must be followed by "**/admin**" to specify the authentication database. After authentication, you can read and write the specific business database. URI example:

```
mongodb://username:password@IP:27017/admin
```

You can also directly access the destination database by specifying a destination database for read and write operation and an additional authentication database parameter (authSource=admin). URI example:

```
mongodb://username:password@IP:27017/somedb?authSource=admin
```

You must use one of the above methods to add admin as an authentication database into the URI.

### Authentication mechanism
MongoDB supports multiple authentication methods. SCRAM-SHA-1 is recommended.
TencentDB for MongoDB supports two authentication methods: "MONGODB-CR" and "SCRAM-SHA-1".
As mentioned above, there are two default users built in TencentDB for MongoDB: "rwuser" and "mongouser", and you can also create additional users in the Console of TencentDB for MongoDB. These users are classified into two types based on the following authentication methods:

| User Name | Authentication Mechanism | Required in URI |
|---------|---------|---------|
| rwuser | MONGODB-CR | The parameter "authMechanism=MONGODB-CR" must be added. |
| mongouser and users created in the console | SCRAM-SHA-1 (recommended) | No parameter needs to be added. |

### Adjust priority for replica set member (Master/Slaves)
TencentDB for MongoDB provides a load balancer IP to access the entire replica set. If you need slave databases to have higher read priority, add the "readPreference" parameter in the URI. Relevant values are described below:

| Value | Description | Default |
|---------|---------|---------|
| primary | Reads master node only | Yes |
| primaryPreferred | Reads master node first. If it is not available, read slave node. |　|
| secondary | Reads slave node only. If it is not available, an error will occur. |　|
| secondaryPreferred | Reads slave node first. If it is not available, read master node. |　|

To set up a priority to read slave node first, you can configure the URI as follows:

```
mongodb://username:password@IP:27017/admin?readPreference=secondaryPreferred
```

## Examples for different Languages

### Shell
[Shell Connection Example](https://cloud.tencent.com/doc/product/240/Shell%E8%BF%9E%E6%8E%A5%E7%A4%BA%E4%BE%8B)
### PHP
[PHP Connection Example](https://cloud.tencent.com/doc/product/240/PHP%E8%BF%9E%E6%8E%A5%E7%A4%BA%E4%BE%8B)
### Node.js
[Node.js Connection Example](https://cloud.tencent.com/doc/product/240/Node.js%E8%BF%9E%E6%8E%A5%E7%A4%BA%E4%BE%8B)
 [mongoose Example](https://cloud.tencent.com/doc/product/240/Node.js%E8%BF%9E%E6%8E%A5%E7%A4%BA%E4%BE%8B#node.js-mongoose-.E8.BF.9E.E6.8E.A5.E7.A4.BA.E4.BE.8B)
### Java
[Java Connection Example](https://cloud.tencent.com/doc/product/240/Java%E8%BF%9E%E6%8E%A5%E7%A4%BA%E4%BE%8B)
### Python
[Python Connection Example](https://cloud.tencent.com/doc/product/240/Python%E8%BF%9E%E6%8E%A5%E7%A4%BA%E4%BE%8B)
### Reconnection mechanism
[Reconnection Mechanism](https://cloud.tencent.com/doc/product/240/4980)

